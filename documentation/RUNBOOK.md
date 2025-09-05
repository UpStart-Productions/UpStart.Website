# UpStart Website — Amplify + Hugo (Blowfish) Runbook

_Last updated: 2025‑09‑04_

This runbook captures the exact, working setup we used to deploy the Hugo + Blowfish site on **AWS Amplify Hosting** with **deterministic builds** and **stable TLS/domain config**. It is designed to work whether the theme is configured as a **Hugo Module** or as a **theme folder**, **without requiring Go** in CI.

---

## 0) Assumptions
- Repo root is the Hugo site (the Amplify clone ends up at `.../src/<hash>/src/UpStart.Website/`).
- Hugo version: **v0.149.0 extended**.
- Theme: **Blowfish** (`github.com/nunocoracao/blowfish`, branch **v2**).
- Hosting: **Amplify Hosting** (which internally uses CloudFront and manages the cert unless you override it).
- DNS: **Route 53**.

---

## 1) The working `amplify.yml` (put at repo root)
This file installs Hugo into a writable path, guarantees the Blowfish theme is present **with or without vendoring**, and forces the theme during the build so Hugo doesn’t try to resolve modules in CI.

```yaml
version: 1
applications:
  - frontend:
      phases:
        preBuild:
          commands:
            # Install Hugo (extended) in a writable path
            - export HUGO_VERSION=${HUGO_VERSION:-0.149.0}
            - curl -sSL -o /tmp/hugo.tar.gz "https://github.com/gohugoio/hugo/releases/download/v${HUGO_VERSION}/hugo_extended_${HUGO_VERSION}_Linux-64bit.tar.gz"
            - mkdir -p "$HOME/bin"
            - tar -xzf /tmp/hugo.tar.gz -C "$HOME/bin" hugo
            - chmod +x "$HOME/bin/hugo"
            - export PATH="$HOME/bin:$PATH"
            - hugo version

            # Optional: install PostCSS deps if present
            - if [ -f package-lock.json ]; then npm ci; fi

            # Ensure Blowfish theme is present WITHOUT Go or rsync
            - set -e
            - VENDOR_PATH="_vendor/github.com/nunocoracao/blowfish/v2"
            - mkdir -p themes
            - |
              if [ -d "$VENDOR_PATH" ]; then
                echo "Using vendored Blowfish from $VENDOR_PATH"
                mkdir -p themes/blowfish
                (cd "$VENDOR_PATH" && tar cf - .) | (cd themes/blowfish && tar xpf -)
              else
                echo "Vendored Blowfish not found; cloning theme"
                git clone --depth 1 --branch v2 https://github.com/nunocoracao/blowfish themes/blowfish \
                  || git clone --depth 1 https://github.com/nunocoracao/blowfish themes/blowfish
              fi
        build:
          commands:
            - echo "Building Hugo site..."
            # Force the theme to avoid any module/theme ambiguity during CI:
            - hugo --minify --theme blowfish
      artifacts:
        baseDirectory: public
        files:
          - '**/*'
      cache:
        paths:
          - node_modules/**/*
          - resources/_gen/**/*
          - _vendor/**/*
          - themes/blowfish/**/*
```

> **Why this works:**  
> - No Go needed in CI.  
> - Uses vendored theme if `_vendor/.../blowfish/v2` exists; otherwise shallow‑clones v2.  
> - `--theme blowfish` removes config ambiguity (no reliance on `theme =` or Hugo Modules resolution in CI).  
> - Installs Hugo to `$HOME/bin` (avoids `/usr/local/bin` permission errors).  
> - Avoids `rsync` (not present in Amplify images) by copying via a `tar` pipe (retains dotfiles).

---

## 2) Optional: Vendor modules locally for faster builds
If you prefer Hugo Modules locally, but do **not** want CI to run `go`:
```bash
cd UpStart.Website
hugo mod tidy
hugo mod vendor
git add _vendor
git commit -m "Vendor Blowfish for CI speed/stability"
git push origin main
```
CI will automatically prefer the vendored copy and skip the `git clone` step.

> If you want to use a pure git submodule instead of Modules, add the theme as a submodule at `themes/blowfish` and remove module imports; keep the YAML above (it will still work).

---

## 3) Domain & TLS with Amplify
**Best practice:** Let Amplify manage the certificate for each domain.

1. **Amplify Console → App → Domain management → Add domain**: `example.com`.  
2. Add **apex** and **www** (set www → apex redirect if desired).  
3. If available, click **Actions → Create records in Route 53**. If not, copy the CloudFront target and create A/AAAA aliases manually:
   - Hosted zone ID for CloudFront alias: `Z2FDTNDATAQYW2`  
   - Point `A` and `AAAA` for apex + `www` to the Amplify CF domain.

4. Confirm SSL is **provisioned/attached** (Amplify managed certificate).  
5. Remove the domain from any **old CloudFront distribution’s** _Alternate domain names (CNAMEs)_ to avoid cert/alias collisions.

---

## 4) Quick verification
```bash
# DNS
dig +short example.com
dig +short www.example.com

# TLS + response
curl -I https://example.com
curl -I https://www.example.com
```

Expect 200/301 with a valid certificate.

---

## 5) Common errors & fixes
- **`tar: hugo: Permission denied`** → You tried extracting to `/usr/local/bin`. Use `$HOME/bin` like the YAML above.  
- **`failed to load modules: module "" not found in "/themes"`** → Hugo can’t find a theme; the YAML above forces `--theme blowfish` and either vendors or clones the theme.  
- **`rsync: command not found`** → Amplify images don’t include `rsync`. The YAML above uses a `tar` pipe instead.  
- **`binary with name "go" not found`** or Go permission errors → Not needed with this setup; avoid `hugo mod` in CI.  
- **`!Failed to set up process.env.secrets`** → Harmless unless you intentionally use SSM secrets at `/amplify/<appId>/<branch>/`.

---

## 6) Rollback / Cleanup
- To revert the theme to a different version: update vendored `_vendor/.../blowfish` locally and commit, **or** change the `git clone --branch` in the YAML.  
- If you previously had a single CloudFront for multiple domains, ensure each domain is only attached to the intended hosting stack (Amplify or its own CF), and remove stragglers from **Alternate domain names**.

---

## 7) One‑time check list
- [ ] `amplify.yml` committed at repo root (exact file above).  
- [ ] Optional: `_vendor/` committed for speed.  
- [ ] Amplify → Domain management shows **green** for apex + www.  
- [ ] Route 53 A/AAAA alias → Amplify’s CloudFront target.  
- [ ] Old CloudFront distribution no longer lists your domain in **Aliases**.

---

**That’s it.** This setup is resilient to the module/submodule toggle, avoids Go in CI, and prevents the common build path and permission pitfalls.
