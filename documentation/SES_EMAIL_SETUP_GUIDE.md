# SES + Gmail Forwarding + Lambda Forwarder Setup Guide

This playbook explains how to set up custom email domains in AWS SES so mail to your domain
(for example `support@yourdomain.com`) forwards into Gmail and you can also **send mail as** that address.

It covers:
- Domain verification (SPF/DKIM/DMARC)
- Inbound routing (SES → S3 → Lambda → Gmail)
- Outbound sending (SES SMTP → Gmail “Send mail as”)
- Optional lifecycle rules for cleanup
- Optional alias mapping for nicer display names

---

## Prerequisites
- Domain hosted in **Route 53**
- Access to **SES** in the same AWS account
- Access to **S3**, **Lambda**, **CloudWatch Logs**

---

## 1. Verify the domain in SES

1. Open SES → **Verified identities** → **Create identity**.
2. Select **Domain**.
3. Enter your domain (e.g. `upstart.solutions`).
4. Enable **Easy DKIM (RSA-2048)**.
5. SES will provide 3 DKIM CNAMEs → add them to Route 53.
6. Add SPF TXT at the root:
   ```
   v=spf1 include:amazonses.com ~all
   ```
7. (Optional) Add DMARC TXT at `_dmarc.yourdomain.com`:
   ```
   v=DMARC1; p=none; rua=mailto:you@gmail.com
   ```
8. Wait until SES shows **Verified**.

---

## 2. Configure inbound mail

1. In Route 53, add MX record at the root:
   ```
   10 inbound-smtp.<region>.amazonaws.com
   ```
   Example (us-west-2):
   ```
   10 inbound-smtp.us-west-2.amazonaws.com
   ```

---

## 3. Create S3 bucket for mail

1. S3 → **Create bucket** → name like `yourdomain-mail`.
2. Block public access ✅.
3. Default encryption ✅.
4. Optional: Use prefix `inbound/` for SES writes.

---

## 4. Create Lambda forwarder

1. Lambda → **Create function**.
   - Name: `ses-forward-to-gmail`
   - Runtime: Python 3.11
   - Architecture: x86_64
   - Permissions: new role
2. Add environment variables:
   - `FORWARD_TO` = your Gmail (e.g. `chiefupstart@gmail.com`)
   - `FORWARD_FROM` = `forwarder@yourdomain.com`
   - (Optional) `ALIAS_MAP_JSON` = `{"support@yourdomain.com":"YourDomain Support","info@yourdomain.com":"YourDomain Info"}`
3. Paste the Python forwarder code into **`lambda_function.py`**.
4. Runtime settings → Handler = `lambda_function.lambda_handler`.
5. Deploy.

### Lambda IAM permissions
Attach inline policy:

```json
{
  "Version": "2012-10-17",
  "Statement": [
    { "Effect": "Allow", "Action": ["ses:SendRawEmail"], "Resource": "*" },
    { "Effect": "Allow", "Action": ["s3:GetObject"], "Resource": "arn:aws:s3:::yourdomain-mail/*" },
    { "Effect": "Allow", "Action": ["logs:CreateLogGroup","logs:CreateLogStream","logs:PutLogEvents"], "Resource": "*" }
  ]
}
```

Also attach managed policy **AWSLambdaBasicExecutionRole**.

---

## 5. Create SES receipt rule

1. SES → **Email receiving → Rule sets**.
2. Create a rule set if none exists → set **Active**.
3. Create new rule:
   - **Recipient condition**: `yourdomain.com` (wildcard for all addresses)
   - **Action**: S3 (bucket = `yourdomain-mail`, prefix = `inbound/`)
   - Stop rule set = Yes
4. Save.

---

## 6. Add S3 event notification → Lambda

1. S3 → your bucket → **Properties → Event notifications**.
2. Create event:
   - Name: `forward-on-create`
   - Event types: All object create events
   - Prefix: `inbound/` (if used)
   - Destination: Lambda → `ses-forward-to-gmail`
3. Save (approve permissions).

---

## 7. Add lifecycle rule (optional)

1. S3 → your bucket → **Management → Lifecycle rules**.
2. Create rule:
   - Name: `delete-after-7d`
   - Scope: prefix `inbound/` (if used)
   - Expiration: delete current objects after 7 days

---

## 8. Verify Gmail (sandbox workaround)

If SES is still in sandbox:
1. SES → **Verified identities → Create identity → Email address**.
2. Enter your Gmail address → click the link SES emails you.
3. Status = Verified → now Lambda can forward to Gmail.
4. (Later) Request **production access** in SES so you don’t need this step.

---

## 9. Set up Gmail “Send mail as”

1. SES → **SMTP settings → Create SMTP credentials**.
   - Save generated **SMTP username** and **SMTP password**.
2. Gmail → Settings → **Accounts and Import → Send mail as → Add another address**:
   - Name: “YourDomain Support”
   - Email: `support@yourdomain.com`
   - Treat as alias: ✅
   - SMTP server: `email-smtp.<region>.amazonaws.com`
   - Port: 587
   - Username: SES SMTP username
   - Password: SES SMTP password
   - TLS: Yes
3. Gmail sends a verification code to `support@yourdomain.com`.
   - It should arrive in Gmail via the forwarder.
   - Enter the code → Confirm

---

## 10. Alias display names (optional)

- The Lambda supports alias → display name mapping.  
- Update `ALIAS_MAP` in code or use an env var:

```json
{"support@yourdomain.com":"YourDomain Support","jeff@yourdomain.com":"Jeff Denton"}
```

- This changes the **From display name** in Gmail.

---

✅ Done! You can now send and receive mail for your domain inside Gmail, with a 7‑day copy kept in S3 for optional future processing.
