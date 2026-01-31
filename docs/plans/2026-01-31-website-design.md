# Floodline Website Design

## Overview

Floodline is a tech consulting business for startups. The website will be a modern, minimal business site with a primary goal of driving contact form submissions.

## Pages

1. **Home** - Hero, value proposition, CTA
2. **About** - Company story, team grid (2-4 people)
3. **Services** - 2 focused service offerings (placeholders)
4. **Contact** - Simple contact form via Formspree

## Visual Design

### Color Palette

| Color | Hex | Usage |
|-------|-----|-------|
| Primary Blue (navy) | #003761 | Primary CTAs, headings, nav |
| Secondary Blue | #3aa2db | Hover states, links, secondary accents |
| Primary Light Brown | #9a8478 | Subtle accents, borders, muted text |
| Prairie Brown | #51453e | Body text (warmer than pure black) |
| Grass Green | #a9b85b | Sparingly for highlights or success states |
| Background | #FFFFFF | Primary background |
| Background Alt | #F8F9FA | Section separation |

### Typography

- **Font:** Inter (Google Fonts)
- **Style:** Sans-serif throughout
- **Approach:** Clean, modern, highly legible

### Design Principles

- Generous whitespace
- Clean lines, no clutter
- Subtle shadows and borders for definition
- Smooth hover states and transitions
- Mobile-first, fully responsive

## Page Details

### Home

**Hero Section:**
- Large, bold headline (placeholder text)
- 1-2 line subheadline
- Primary CTA: "Get in Touch" → Contact page
- White background, navy text, navy button

**Value Proposition Section:**
- 3 points in horizontal row (stacks on mobile)
- Simple icon + title + one-line description each
- Light gray background for visual separation

**Footer CTA:**
- "Ready to talk?" with button to Contact

**Footer:**
- Minimal: copyright, nav links, optional social icons
- Navy background with white text

### About

**Company Section:**
- Short intro paragraph about mission/approach
- Placeholder text to customize

**Team Section:**
- Grid layout: 2 columns desktop, 1 column mobile
- Team member cards:
  - Circular/rounded photo
  - Name (navy)
  - Role (gray)
  - 2-3 line bio
- Subtle shadow or border on cards

**Bottom CTA:**
- Link to Contact page

### Services

**Layout:**
- Page heading
- 2 service blocks, stacked vertically

**Service Block:**
- Service title (large, navy)
- 2-3 paragraph description
- Optional bullet points
- Card-style with subtle shadow

**Bottom CTA:**
- "Let's discuss your needs" → Contact

### Contact

**Intro:**
- Heading: "Get in Touch"
- Brief intro line

**Form (via Formspree):**
- Name (required)
- Email (required)
- Message (textarea, required)
- Submit button (navy with white text)

**Fallback:**
- Email address displayed below form

## Technical Stack

- **Static Site Generator:** Jekyll
- **Styling:** Custom CSS (replacing Minima defaults)
- **Font:** Inter via Google Fonts
- **Form Backend:** Formspree
- **Responsive:** Mobile-first approach

## Responsive Behavior

- Hamburger navigation on mobile
- Stacked layouts for all grid content
- Touch-friendly tap targets
- Readable font sizes at all breakpoints
