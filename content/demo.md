---
title: "Blowfish Images Demo"
description: "Showcasing how to use images in Blowfish components"
layout: "simple"
---

# Blowfish Images Demo

This page shows you how to use images in different Blowfish components and where they appear.

## 🖼️ Author Profile Image

The author profile image appears in the **Profile Layout** homepage and in article author sections.

**Location**: `config/_default/languages.en.toml`
```toml
[params.author]
image = "img/avatar.png"
```

**What you see**: A circular avatar image in the author profile card.

## 📸 Featured Images for Articles

Featured images appear in article headers, card views, and social media previews.

**Location**: Article front matter
```yaml
---
title: "My Article"
featuredImage: "img/my-image.jpg"
---
```

**What you see**: 
- Hero image at the top of articles
- Thumbnail in card views
- Social media preview images

## 🎨 Homepage Background Images

Background images can be used in different homepage layouts.

**Location**: `config/_default/params.toml`
```toml
[params.homepage]
  layout = "background"
  homepageImage = "img/hero.jpg"
```

**What you see**: Full-screen background image with blur effects.

## 📱 Hero Layout Images

Hero layout uses a prominent image with the hero content.

**Location**: `config/_default/params.toml`
```toml
[params.homepage]
  layout = "hero"
  homepageImage = "img/hero.jpg"
```

**What you see**: Large hero image with overlaid text and buttons.

## 🎪 Gallery Shortcode

Blowfish includes a gallery shortcode for displaying multiple images.

```markdown
{{< gallery >}}
  <img src="img/image1.jpg" class="grid-w33" />
  <img src="img/image2.jpg" class="grid-w33" />
  <img src="img/image3.jpg" class="grid-w33" />
{{< /gallery >}}
```

**What you see**: Responsive image grid with hover effects.

## 🎠 Carousel Shortcode

Carousel for displaying images in a slideshow.

```markdown
{{< carousel images="img/slide1.jpg,img/slide2.jpg,img/slide3.jpg" >}}
```

**What you see**: Interactive image carousel with navigation.

## 📊 List Card Images

Images in list cards for better visual appeal.

**Location**: Article front matter
```yaml
---
title: "Article Title"
featuredImage: "img/card-image.jpg"
---
```

**What you see**: Card thumbnails in list views.

## 🔧 Image Configuration Options

### Image Optimization
```toml
[params]
  disableImageOptimization = false  # Enable/disable image processing
```

### Default Images
```toml
[params]
  defaultBackgroundImage = "img/default-bg.jpg"
  defaultFeaturedImage = "img/default-featured.jpg"
  defaultSocialImage = "img/default-social.jpg"
```

### Background Image Settings
```toml
[params.homepage]
  layoutBackgroundBlur = true        # Blur effect on scroll
  disableHeroImageFilter = false     # Disable image filters
```

## 📁 Image File Structure

```
static/
└── img/
    ├── avatar.png          # Author profile
    ├── hero.jpg           # Homepage background
    ├── featured-1.jpg     # Article featured images
    ├── featured-2.jpg
    └── gallery/           # Gallery images
        ├── image1.jpg
        ├── image2.jpg
        └── image3.jpg
```

## 🎯 Where Images Appear

1. **Homepage Profile Layout**: Author avatar, social media icons
2. **Article Pages**: Featured image hero, author avatar
3. **List Pages**: Card thumbnails, grid layouts
4. **Search Results**: Article previews with images
5. **Social Media**: Open Graph and Twitter Card images
6. **Navigation**: Logo images (if configured)

## 🚀 Best Practices

- **Optimize images** before uploading (compress, resize)
- **Use descriptive filenames** (e.g., `nepho-app-screenshot.jpg`)
- **Consistent aspect ratios** for card images
- **Alt text** for accessibility
- **WebP format** for better performance

---

**Current Demo Images**: The images you see on this site are placeholder SVGs. Replace them with real images to see the full visual impact of Blowfish components!

Visit the [homepage](/) to see the author avatar, or check out the [blog posts](/posts) to see featured images in action.
