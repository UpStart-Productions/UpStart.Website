---
title: "Demo Page"
description: "Showcasing Blowfish components and features"
---

# Demo Page

This page showcases various Blowfish components and features.

## Text Components

### Headings
# Heading 1
## Heading 2
### Heading 3
#### Heading 4
##### Heading 5
###### Heading 6

### Text Formatting
**Bold text** and *italic text* and `inline code`.

### Lists
- Unordered list item 1
- Unordered list item 2
  - Nested item
  - Another nested item
- Unordered list item 3

1. Ordered list item 1
2. Ordered list item 2
3. Ordered list item 3

### Blockquotes
> This is a blockquote. It can span multiple lines and contain **bold** or *italic* text.

### Code Blocks
```javascript
function hello() {
  console.log("Hello, world!");
}
```

## Blowfish Components

### Alerts
{{< alert >}}
**Info Alert:** This is an info alert with some important information.
{{< /alert >}}

{{< alert icon="fire" cardColor="#e63946" iconColor="#1d3557" textColor="#f1faee" >}}
**Warning Alert:** This is a warning alert with a caution message.
{{< /alert >}}

{{< alert icon="star" cardColor="#059669" iconColor="#ffffff" textColor="#ffffff" >}}
**Success Alert:** This is a success alert confirming an action was completed.
{{< /alert >}}

### Badges
{{< badge >}}New Feature!{{< /badge >}}

{{< badge >}}Updated{{< /badge >}}

{{< badge >}}Popular{{< /badge >}}

### Buttons
{{< button href="/contact" target="_self" >}}
Get Started
{{< /button >}}

{{< button href="/about" target="_self" >}}
Learn More
{{< /button >}}

### Keywords
{{< keywordList >}}
{{< keyword icon="github" >}}Web Development{{< /keyword >}}
{{< keyword icon="code" >}}**Product Design**{{< /keyword >}}
{{< keyword icon="star" >}}*Custom Apps*{{< /keyword >}}
{{< /keywordList >}}

### Lead Text
{{< lead >}}
This is lead text that emphasizes important introductory information. It's styled to stand out from regular content.
{{< /lead >}}

### TypeIt Animation
{{< typeit >}}
Welcome to our demo page!
{{< /typeit >}}

### Timeline
{{< timeline >}}

{{< timelineItem icon="github" header="Web Development" badge="2024" subheader="Modern web solutions" >}}
Custom websites and web applications built with modern technologies for optimal performance and user experience.
{{< /timelineItem >}}

{{< timelineItem icon="code" header="Product Design" badge="2024" subheader="User-centered design" >}}
User-centered design that creates meaningful connections between your brand and your customers.
{{< /timelineItem >}}

{{< timelineItem icon="star" header="Custom Apps" badge="2024" subheader="Mobile & web applications" >}}
Native and cross-platform mobile applications that deliver exceptional user experiences.
{{< /timelineItem >}}

{{< /timeline >}}

### Color Swatches
{{< swatches "#0ea5e9" "#10b981" "#f59e0b" >}}

## Advanced Features

### Math (if enabled)
Inline math: $E = mc^2$

Block math:
$$
\int_{-\infty}^{\infty} e^{-x^2} dx = \sqrt{\pi}
$$

## Conclusion

This demo page shows many of the components available in Blowfish. You can use these components throughout your site to create rich, interactive content.
