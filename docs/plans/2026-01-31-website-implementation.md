# Floodline Website Implementation Plan

> **For Claude:** REQUIRED SUB-SKILL: Use superpowers:executing-plans to implement this plan task-by-task.

**Goal:** Build a modern, minimal business website for Floodline tech consulting using Jekyll with custom styling.

**Architecture:** Replace Minima theme defaults with custom layouts and SCSS. Create four pages (Home, About, Services, Contact) with shared header/footer includes and consistent branding.

**Tech Stack:** Jekyll, Custom SCSS, Inter font (Google Fonts), Formspree for contact form.

---

## Task 1: Configure Site Settings

**Files:**
- Modify: `_config.yml`

**Step 1: Update _config.yml with Floodline branding**

```yaml
title: Floodline
email: hello@floodline.co
description: >-
  Technology consulting for ambitious startups. We help founders build
  the right thing, the right way.
baseurl: ""
url: ""

# Build settings
plugins:
  - jekyll-feed

# Custom variables
colors:
  primary_blue: "#003761"
  secondary_blue: "#3aa2db"
  light_brown: "#9a8478"
  prairie_brown: "#51453e"
  grass_green: "#a9b85b"

# Exclude theme default
theme: null

# Sass config
sass:
  style: compressed
```

**Step 2: Commit**

```bash
git add _config.yml
git commit -m "Configure site settings and branding"
```

---

## Task 2: Create Base Layout and Includes

**Files:**
- Create: `_layouts/default.html`
- Create: `_includes/head.html`
- Create: `_includes/header.html`
- Create: `_includes/footer.html`

**Step 1: Create _layouts directory and default.html**

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    {% include head.html %}
  </head>
  <body>
    {% include header.html %}
    <main>
      {{ content }}
    </main>
    {% include footer.html %}
  </body>
</html>
```

**Step 2: Create _includes/head.html**

```html
<meta charset="utf-8">
<meta name="viewport" content="width=device-width, initial-scale=1">
<title>{% if page.title %}{{ page.title }} | {% endif %}{{ site.title }}</title>
<meta name="description" content="{{ page.description | default: site.description }}">
<link rel="preconnect" href="https://fonts.googleapis.com">
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
<link href="https://fonts.googleapis.com/css2?family=Inter:wght@400;500;600;700&display=swap" rel="stylesheet">
<link rel="stylesheet" href="{{ '/assets/css/main.css' | relative_url }}">
```

**Step 3: Create _includes/header.html**

```html
<header class="site-header">
  <div class="container">
    <a href="{{ '/' | relative_url }}" class="logo">Floodline</a>
    <button class="nav-toggle" aria-label="Toggle navigation">
      <span></span>
      <span></span>
      <span></span>
    </button>
    <nav class="site-nav">
      <a href="{{ '/' | relative_url }}" {% if page.url == '/' %}class="active"{% endif %}>Home</a>
      <a href="{{ '/about/' | relative_url }}" {% if page.url == '/about/' %}class="active"{% endif %}>About</a>
      <a href="{{ '/services/' | relative_url }}" {% if page.url == '/services/' %}class="active"{% endif %}>Services</a>
      <a href="{{ '/contact/' | relative_url }}" {% if page.url == '/contact/' %}class="active"{% endif %}>Contact</a>
    </nav>
  </div>
</header>
```

**Step 4: Create _includes/footer.html**

```html
<footer class="site-footer">
  <div class="container">
    <div class="footer-content">
      <div class="footer-brand">
        <span class="logo">Floodline</span>
        <p>&copy; {{ 'now' | date: '%Y' }} Floodline. All rights reserved.</p>
      </div>
      <nav class="footer-nav">
        <a href="{{ '/' | relative_url }}">Home</a>
        <a href="{{ '/about/' | relative_url }}">About</a>
        <a href="{{ '/services/' | relative_url }}">Services</a>
        <a href="{{ '/contact/' | relative_url }}">Contact</a>
      </nav>
    </div>
  </div>
</footer>
```

**Step 5: Commit**

```bash
git add _layouts/default.html _includes/head.html _includes/header.html _includes/footer.html
git commit -m "Add base layout and header/footer includes"
```

---

## Task 3: Create SCSS Stylesheets

**Files:**
- Create: `_sass/_variables.scss`
- Create: `_sass/_base.scss`
- Create: `_sass/_layout.scss`
- Create: `_sass/_components.scss`
- Create: `assets/css/main.scss`

**Step 1: Create _sass/_variables.scss**

```scss
// Colors
$primary-blue: #003761;
$secondary-blue: #3aa2db;
$light-brown: #9a8478;
$prairie-brown: #51453e;
$grass-green: #a9b85b;
$white: #ffffff;
$bg-alt: #f8f9fa;

// Typography
$font-family: 'Inter', -apple-system, BlinkMacSystemFont, 'Segoe UI', sans-serif;
$font-size-base: 1rem;
$font-size-lg: 1.125rem;
$font-size-xl: 1.5rem;
$font-size-2xl: 2rem;
$font-size-3xl: 2.5rem;
$font-size-4xl: 3rem;
$line-height-base: 1.6;
$line-height-tight: 1.2;

// Spacing
$space-xs: 0.5rem;
$space-sm: 1rem;
$space-md: 1.5rem;
$space-lg: 2rem;
$space-xl: 3rem;
$space-2xl: 4rem;
$space-3xl: 6rem;

// Layout
$container-max: 1200px;
$container-padding: 1.5rem;

// Breakpoints
$breakpoint-sm: 640px;
$breakpoint-md: 768px;
$breakpoint-lg: 1024px;

// Shadows
$shadow-sm: 0 1px 2px rgba(0, 0, 0, 0.05);
$shadow-md: 0 4px 6px rgba(0, 0, 0, 0.07);
$shadow-lg: 0 10px 15px rgba(0, 0, 0, 0.1);

// Transitions
$transition-fast: 150ms ease;
$transition-base: 200ms ease;
```

**Step 2: Create _sass/_base.scss**

```scss
*,
*::before,
*::after {
  box-sizing: border-box;
  margin: 0;
  padding: 0;
}

html {
  font-size: 16px;
  scroll-behavior: smooth;
}

body {
  font-family: $font-family;
  font-size: $font-size-base;
  line-height: $line-height-base;
  color: $prairie-brown;
  background-color: $white;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
}

h1, h2, h3, h4, h5, h6 {
  color: $primary-blue;
  line-height: $line-height-tight;
  font-weight: 600;
}

h1 { font-size: $font-size-4xl; }
h2 { font-size: $font-size-3xl; }
h3 { font-size: $font-size-2xl; }
h4 { font-size: $font-size-xl; }

@media (max-width: $breakpoint-md) {
  h1 { font-size: $font-size-3xl; }
  h2 { font-size: $font-size-2xl; }
  h3 { font-size: $font-size-xl; }
}

a {
  color: $secondary-blue;
  text-decoration: none;
  transition: color $transition-fast;

  &:hover {
    color: $primary-blue;
  }
}

img {
  max-width: 100%;
  height: auto;
  display: block;
}

.container {
  max-width: $container-max;
  margin: 0 auto;
  padding: 0 $container-padding;
}
```

**Step 3: Create _sass/_layout.scss**

```scss
// Header
.site-header {
  padding: $space-md 0;
  background: $white;
  border-bottom: 1px solid rgba($light-brown, 0.2);
  position: sticky;
  top: 0;
  z-index: 100;

  .container {
    display: flex;
    justify-content: space-between;
    align-items: center;
  }

  .logo {
    font-size: $font-size-xl;
    font-weight: 700;
    color: $primary-blue;
    text-decoration: none;
  }
}

.nav-toggle {
  display: none;
  flex-direction: column;
  gap: 5px;
  background: none;
  border: none;
  cursor: pointer;
  padding: $space-xs;

  span {
    display: block;
    width: 24px;
    height: 2px;
    background: $primary-blue;
    transition: transform $transition-base;
  }

  @media (max-width: $breakpoint-md) {
    display: flex;
  }
}

.site-nav {
  display: flex;
  gap: $space-lg;

  a {
    color: $prairie-brown;
    font-weight: 500;
    transition: color $transition-fast;

    &:hover,
    &.active {
      color: $primary-blue;
    }
  }

  @media (max-width: $breakpoint-md) {
    display: none;
    position: absolute;
    top: 100%;
    left: 0;
    right: 0;
    background: $white;
    flex-direction: column;
    padding: $space-md $container-padding;
    gap: $space-md;
    border-bottom: 1px solid rgba($light-brown, 0.2);

    &.open {
      display: flex;
    }
  }
}

// Footer
.site-footer {
  background: $primary-blue;
  color: $white;
  padding: $space-xl 0;
  margin-top: $space-3xl;

  .logo {
    font-size: $font-size-lg;
    font-weight: 700;
    color: $white;
  }

  p {
    color: rgba($white, 0.7);
    font-size: 0.875rem;
    margin-top: $space-xs;
  }
}

.footer-content {
  display: flex;
  justify-content: space-between;
  align-items: flex-start;
  flex-wrap: wrap;
  gap: $space-lg;
}

.footer-nav {
  display: flex;
  gap: $space-md;

  a {
    color: rgba($white, 0.8);
    font-size: 0.875rem;

    &:hover {
      color: $white;
    }
  }
}

// Main content
main {
  min-height: calc(100vh - 200px);
}

// Section spacing
.section {
  padding: $space-3xl 0;

  &--alt {
    background: $bg-alt;
  }
}

.section-header {
  text-align: center;
  margin-bottom: $space-xl;

  h2 {
    margin-bottom: $space-sm;
  }

  p {
    color: $light-brown;
    font-size: $font-size-lg;
    max-width: 600px;
    margin: 0 auto;
  }
}
```

**Step 4: Create _sass/_components.scss**

```scss
// Buttons
.btn {
  display: inline-block;
  padding: $space-sm $space-lg;
  font-family: $font-family;
  font-size: $font-size-base;
  font-weight: 500;
  text-decoration: none;
  border-radius: 6px;
  border: none;
  cursor: pointer;
  transition: all $transition-fast;

  &--primary {
    background: $primary-blue;
    color: $white;

    &:hover {
      background: darken($primary-blue, 8%);
      color: $white;
    }
  }

  &--secondary {
    background: transparent;
    color: $primary-blue;
    border: 2px solid $primary-blue;

    &:hover {
      background: $primary-blue;
      color: $white;
    }
  }
}

// Hero
.hero {
  padding: $space-3xl 0;
  text-align: center;

  h1 {
    margin-bottom: $space-md;
    max-width: 800px;
    margin-left: auto;
    margin-right: auto;
  }

  p {
    font-size: $font-size-lg;
    color: $light-brown;
    max-width: 600px;
    margin: 0 auto $space-lg;
  }
}

// Value Props
.value-props {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  gap: $space-lg;

  @media (max-width: $breakpoint-md) {
    grid-template-columns: 1fr;
  }
}

.value-prop {
  text-align: center;
  padding: $space-lg;

  .icon {
    width: 48px;
    height: 48px;
    margin: 0 auto $space-md;
    color: $secondary-blue;
  }

  h3 {
    font-size: $font-size-lg;
    margin-bottom: $space-sm;
  }

  p {
    color: $light-brown;
  }
}

// CTA Section
.cta-section {
  text-align: center;
  padding: $space-3xl 0;

  h2 {
    margin-bottom: $space-md;
  }
}

// Cards
.card {
  background: $white;
  border-radius: 8px;
  padding: $space-lg;
  box-shadow: $shadow-md;
  border: 1px solid rgba($light-brown, 0.1);
}

// Team Grid
.team-grid {
  display: grid;
  grid-template-columns: repeat(2, 1fr);
  gap: $space-lg;

  @media (max-width: $breakpoint-md) {
    grid-template-columns: 1fr;
  }
}

.team-member {
  text-align: center;

  .photo {
    width: 120px;
    height: 120px;
    border-radius: 50%;
    object-fit: cover;
    margin: 0 auto $space-md;
    background: $bg-alt;
  }

  h3 {
    font-size: $font-size-lg;
    margin-bottom: $space-xs;
  }

  .role {
    color: $light-brown;
    font-size: 0.875rem;
    margin-bottom: $space-sm;
  }

  p {
    font-size: 0.9375rem;
  }
}

// Service Cards
.services-list {
  display: flex;
  flex-direction: column;
  gap: $space-lg;
}

.service-card {
  h3 {
    margin-bottom: $space-sm;
  }

  p {
    margin-bottom: $space-sm;
  }

  ul {
    margin-left: $space-md;
    color: $prairie-brown;

    li {
      margin-bottom: $space-xs;
    }
  }
}

// Contact Form
.contact-form {
  max-width: 600px;
  margin: 0 auto;

  .form-group {
    margin-bottom: $space-md;

    label {
      display: block;
      font-weight: 500;
      margin-bottom: $space-xs;
      color: $prairie-brown;
    }

    input,
    textarea {
      width: 100%;
      padding: $space-sm;
      font-family: $font-family;
      font-size: $font-size-base;
      border: 1px solid rgba($light-brown, 0.3);
      border-radius: 6px;
      transition: border-color $transition-fast;

      &:focus {
        outline: none;
        border-color: $secondary-blue;
      }
    }

    textarea {
      min-height: 150px;
      resize: vertical;
    }
  }

  button {
    width: 100%;
  }
}

.contact-fallback {
  text-align: center;
  margin-top: $space-lg;
  color: $light-brown;

  a {
    font-weight: 500;
  }
}

// Page Header
.page-header {
  padding: $space-xl 0;
  text-align: center;
  border-bottom: 1px solid rgba($light-brown, 0.1);

  h1 {
    margin-bottom: $space-sm;
  }

  p {
    color: $light-brown;
    font-size: $font-size-lg;
  }
}

// About content
.about-content {
  max-width: 700px;
  margin: 0 auto;

  p {
    margin-bottom: $space-md;
  }
}
```

**Step 5: Create assets/css/main.scss**

```scss
---
---

@import "variables";
@import "base";
@import "layout";
@import "components";
```

**Step 6: Commit**

```bash
git add _sass assets/css/main.scss
git commit -m "Add SCSS stylesheets with brand colors and components"
```

---

## Task 4: Create Page Layout

**Files:**
- Create: `_layouts/page.html`

**Step 1: Create _layouts/page.html**

```html
---
layout: default
---

<div class="page-header">
  <div class="container">
    <h1>{{ page.title }}</h1>
    {% if page.subtitle %}
    <p>{{ page.subtitle }}</p>
    {% endif %}
  </div>
</div>

<div class="section">
  <div class="container">
    {{ content }}
  </div>
</div>
```

**Step 2: Commit**

```bash
git add _layouts/page.html
git commit -m "Add page layout"
```

---

## Task 5: Create Home Page

**Files:**
- Modify: `index.markdown` → rename to `index.html`

**Step 1: Delete old index.markdown and create index.html**

```html
---
layout: default
title: Home
---

<section class="hero">
  <div class="container">
    <h1>Technology consulting for ambitious startups</h1>
    <p>We help founders build the right thing, the right way. From technical strategy to hands-on implementation.</p>
    <a href="{{ '/contact/' | relative_url }}" class="btn btn--primary">Get in Touch</a>
  </div>
</section>

<section class="section section--alt">
  <div class="container">
    <div class="value-props">
      <div class="value-prop">
        <svg class="icon" xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke="currentColor">
          <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M9 19v-6a2 2 0 00-2-2H5a2 2 0 00-2 2v6a2 2 0 002 2h2a2 2 0 002-2zm0 0V9a2 2 0 012-2h2a2 2 0 012 2v10m-6 0a2 2 0 002 2h2a2 2 0 002-2m0 0V5a2 2 0 012-2h2a2 2 0 012 2v14a2 2 0 01-2 2h-2a2 2 0 01-2-2z" />
        </svg>
        <h3>Strategic Guidance</h3>
        <p>Make confident technology decisions with experienced advisors who've been there.</p>
      </div>
      <div class="value-prop">
        <svg class="icon" xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke="currentColor">
          <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M10 20l4-16m4 4l4 4-4 4M6 16l-4-4 4-4" />
        </svg>
        <h3>Hands-on Support</h3>
        <p>We roll up our sleeves and work alongside your team to get things done.</p>
      </div>
      <div class="value-prop">
        <svg class="icon" xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke="currentColor">
          <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M13 10V3L4 14h7v7l9-11h-7z" />
        </svg>
        <h3>Startup Experience</h3>
        <p>We understand the pace and constraints of early-stage companies.</p>
      </div>
    </div>
  </div>
</section>

<section class="cta-section">
  <div class="container">
    <h2>Ready to talk?</h2>
    <p>Let's discuss how we can help your startup succeed.</p>
    <a href="{{ '/contact/' | relative_url }}" class="btn btn--primary">Contact Us</a>
  </div>
</section>
```

**Step 2: Commit**

```bash
rm index.markdown
git add index.html
git commit -m "Create home page with hero and value props"
```

---

## Task 6: Create About Page

**Files:**
- Modify: `about.markdown` → rename to `about.html`

**Step 1: Delete old about.markdown and create about.html**

```html
---
layout: default
title: About
permalink: /about/
---

<div class="page-header">
  <div class="container">
    <h1>About Floodline</h1>
    <p>Technology partners for ambitious startups</p>
  </div>
</div>

<section class="section">
  <div class="container">
    <div class="about-content">
      <p>Floodline was founded with a simple belief: startups deserve access to experienced technology leadership without the overhead of full-time hires.</p>
      <p>We partner with founders at critical moments—when you're making foundational technology decisions, scaling your team, or navigating complex technical challenges. Our hands-on approach means we're not just advisors; we're collaborators who understand the urgency and constraints of early-stage companies.</p>
      <p>Based on the Canadian prairies, we bring a grounded, no-nonsense approach to technology consulting. We focus on what matters and skip the rest.</p>
    </div>
  </div>
</section>

<section class="section section--alt">
  <div class="container">
    <div class="section-header">
      <h2>The Team</h2>
    </div>
    <div class="team-grid">
      <div class="team-member card">
        <div class="photo"></div>
        <h3>Team Member Name</h3>
        <p class="role">Role / Title</p>
        <p>Brief bio about this team member. Their background, expertise, and what they bring to Floodline.</p>
      </div>
      <div class="team-member card">
        <div class="photo"></div>
        <h3>Team Member Name</h3>
        <p class="role">Role / Title</p>
        <p>Brief bio about this team member. Their background, expertise, and what they bring to Floodline.</p>
      </div>
    </div>
  </div>
</section>

<section class="cta-section">
  <div class="container">
    <h2>Want to work with us?</h2>
    <a href="{{ '/contact/' | relative_url }}" class="btn btn--primary">Get in Touch</a>
  </div>
</section>
```

**Step 2: Commit**

```bash
rm about.markdown
git add about.html
git commit -m "Create about page with team section"
```

---

## Task 7: Create Services Page

**Files:**
- Create: `services.html`

**Step 1: Create services.html**

```html
---
layout: default
title: Services
permalink: /services/
---

<div class="page-header">
  <div class="container">
    <h1>Services</h1>
    <p>How we help startups succeed</p>
  </div>
</div>

<section class="section">
  <div class="container">
    <div class="services-list">
      <div class="service-card card">
        <h3>Service One</h3>
        <p>Description of your first core service offering. Explain what it includes, who it's for, and what outcomes clients can expect.</p>
        <p>Add more detail here about the approach, methodology, or specific deliverables.</p>
        <ul>
          <li>Key deliverable or feature</li>
          <li>Another key aspect</li>
          <li>Third important element</li>
        </ul>
      </div>
      <div class="service-card card">
        <h3>Service Two</h3>
        <p>Description of your second core service offering. Explain what it includes, who it's for, and what outcomes clients can expect.</p>
        <p>Add more detail here about the approach, methodology, or specific deliverables.</p>
        <ul>
          <li>Key deliverable or feature</li>
          <li>Another key aspect</li>
          <li>Third important element</li>
        </ul>
      </div>
    </div>
  </div>
</section>

<section class="cta-section section--alt">
  <div class="container">
    <h2>Let's discuss your needs</h2>
    <p>Every startup is different. Let's talk about how we can help yours.</p>
    <a href="{{ '/contact/' | relative_url }}" class="btn btn--primary">Contact Us</a>
  </div>
</section>
```

**Step 2: Commit**

```bash
git add services.html
git commit -m "Create services page with placeholder content"
```

---

## Task 8: Create Contact Page

**Files:**
- Create: `contact.html`

**Step 1: Create contact.html**

```html
---
layout: default
title: Contact
permalink: /contact/
---

<div class="page-header">
  <div class="container">
    <h1>Get in Touch</h1>
    <p>Tell us about your project and we'll be in touch.</p>
  </div>
</div>

<section class="section">
  <div class="container">
    <form class="contact-form" action="https://formspree.io/f/YOUR_FORM_ID" method="POST">
      <div class="form-group">
        <label for="name">Name</label>
        <input type="text" id="name" name="name" required>
      </div>
      <div class="form-group">
        <label for="email">Email</label>
        <input type="email" id="email" name="email" required>
      </div>
      <div class="form-group">
        <label for="message">Message</label>
        <textarea id="message" name="message" required></textarea>
      </div>
      <button type="submit" class="btn btn--primary">Send Message</button>
    </form>
    <p class="contact-fallback">Or email us directly at <a href="mailto:{{ site.email }}">{{ site.email }}</a></p>
  </div>
</section>
```

**Step 2: Commit**

```bash
git add contact.html
git commit -m "Create contact page with Formspree form"
```

---

## Task 9: Add Mobile Navigation JavaScript

**Files:**
- Create: `assets/js/main.js`
- Modify: `_includes/head.html`

**Step 1: Create assets/js/main.js**

```javascript
document.addEventListener('DOMContentLoaded', function() {
  const navToggle = document.querySelector('.nav-toggle');
  const siteNav = document.querySelector('.site-nav');

  if (navToggle && siteNav) {
    navToggle.addEventListener('click', function() {
      siteNav.classList.toggle('open');
      navToggle.classList.toggle('active');
    });
  }
});
```

**Step 2: Add script tag to _includes/head.html (before closing)**

Add to bottom of head.html:
```html
<script src="{{ '/assets/js/main.js' | relative_url }}" defer></script>
```

**Step 3: Commit**

```bash
git add assets/js/main.js _includes/head.html
git commit -m "Add mobile navigation toggle"
```

---

## Task 10: Clean Up and Test

**Files:**
- Delete: `_posts/2026-01-30-welcome-to-jekyll.markdown`
- Delete: `404.html` (optional: keep or restyle)

**Step 1: Remove default Jekyll post**

```bash
rm _posts/2026-01-30-welcome-to-jekyll.markdown
rmdir _posts
```

**Step 2: Build and verify site**

```bash
bundle exec jekyll serve
```

Open http://localhost:4000 and verify:
- All four pages load
- Navigation works (including mobile toggle)
- Styling matches design spec
- Contact form displays correctly

**Step 3: Final commit**

```bash
git add -A
git commit -m "Clean up default Jekyll files"
```

---

## Summary

| Task | Description |
|------|-------------|
| 1 | Configure site settings |
| 2 | Create base layout and includes |
| 3 | Create SCSS stylesheets |
| 4 | Create page layout |
| 5 | Create home page |
| 6 | Create about page |
| 7 | Create services page |
| 8 | Create contact page |
| 9 | Add mobile navigation |
| 10 | Clean up and test |

After completing all tasks, you'll have a fully functional Floodline website with:
- Custom branding and color palette
- Responsive design with mobile navigation
- Four pages: Home, About, Services, Contact
- Contact form via Formspree
- Placeholder content ready for customization
