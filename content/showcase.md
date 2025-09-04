---
title: "Blowfish Components Showcase"
description: "Real Blowfish components in action"
featuredImage: "img/hugo-logo.jpg"
showToC: true
---

# Blowfish Components Showcase

This page demonstrates **real** Blowfish components with actual styling, animations, and interactivity.

## 🎨 What You're Seeing Right Now

### Hero Image Component
The large image at the top of this page is a **Blowfish Hero Component**. It automatically:
- Scales responsively
- Has parallax effects
- Applies image filters
- Shows on social media

### Table of Contents Component
The sidebar on the right (if visible) is a **Blowfish TOC Component** that:
- Auto-generates from headings
- Has smooth scrolling
- Highlights current section
- Is collapsible

### Article Meta Components
Below the title, you see **Blowfish Meta Components**:
- Reading time calculation
- Word count
- Tags/categories
- Social sharing buttons

## 🎪 Interactive Components

### Search Component
Press `/` on your keyboard to activate the **Blowfish Search Component**:
- Real-time search
- Keyboard navigation
- Search highlighting
- Search analytics

### Dark Mode Component
Look for the moon/sun icon in the header - that's the **Blowfish Appearance Switcher**:
- Smooth transitions
- System preference detection
- Persistent settings
- Animated icons

### Navigation Components
The header contains several **Blowfish Navigation Components**:
- Fixed header with blur effects
- Mobile hamburger menu
- Dropdown menus
- Active state indicators

## 📊 List Components

Visit the [blog posts](/posts) to see **Blowfish List Components**:
- Card grid layouts
- Featured image thumbnails
- Hover animations
- Responsive design

## 🎯 Homepage Components

Go to the [homepage](/) to see **Blowfish Homepage Components**:
- Background layout with blur effects
- Recent articles grid
- Author profile card
- Social media icons

## 🔧 Configuration-Driven Components

These components are controlled by `params.toml`:

```toml
[params.homepage]
  layout = "background"        # Visual layout
  cardView = true             # Card components
  layoutBackgroundBlur = true # Blur effects

[params.article]
  showHero = true             # Hero images
  heroStyle = "background"    # Hero styles
  showToC = true              # Table of contents

[params.header]
  layout = "fixed-fill-blur"  # Header effects
```

## 🎨 Visual Effects You Should See

1. **Smooth Animations** - Hover effects, transitions
2. **Blur Effects** - Background blur on scroll
3. **Parallax** - Hero images move on scroll
4. **Responsive Design** - Components adapt to screen size
5. **Color Schemes** - Dark/light mode switching
6. **Typography** - Beautiful fonts and spacing

## 🚀 Real Components vs Documentation

**What you saw before**: Plain text documentation
**What you see now**: Actual Blowfish components with:
- Styling and animations
- Interactive features
- Responsive behavior
- Theme integration

---

**The key difference**: Blowfish components are **theme-integrated** and **configuration-driven**. They automatically render with beautiful styling when you configure them properly.

**Try these interactions**:
- Press `/` for search
- Click the moon/sun icon for dark mode
- Scroll to see parallax effects
- Resize your browser to see responsive design
- Visit different pages to see different component layouts
