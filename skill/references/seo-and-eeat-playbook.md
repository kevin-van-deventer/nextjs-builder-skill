---
name: "SEO & E-E-A-T Content Strategy Playbook"
creator: "Kevin & Eduard"
version: "1.3.0"
last_updated: "2026-05-20"
description: "Guidelines and checklist specifications for technical SEO, Google E-E-A-T standards, dynamic JSON-LD schemas, and Generative Engine Optimization (GEO)."
---

# 🔍 SEO & E-E-A-T Content Strategy Playbook

This document defines our technical search engine optimization practices, content hierarchy formats, asset optimization rules, dynamic schema templates, and Google E-E-A-T compliance guidelines.

---

## 📝 1. Per-Page SEO Checklist
Apply this checklist to **EVERY** page you create. No exceptions.

### A. Title Tag
*   **Uniqueness**: Unique across the entire site.
*   **Keyword Focus**: Contains primary keyword, ideally near the start.
*   **Length**: Under 60 characters.
*   **Format**: `"Primary Keyword | Brand Name"` or `"Primary Keyword — Brand Name"`.
*   **CTR Optimization**: Compelling to click — think of it as an ad headline.

### B. Meta Description
*   **Uniqueness**: Unique across the entire site.
*   **Keyword Focus**: Contains primary keyword naturally.
*   **Length**: Under 160 characters.
*   **Actionable Copy**: Includes a call to action or value proposition.
*   **CTR Optimization**: Written to increase click-through rate from search results.

### C. URL Slug
*   **Structure**: Short, descriptive, lowercase.
*   **Keyword Focus**: Contains primary keyword.
*   **Separators**: Uses hyphens (`-`), never underscores (`_`).
*   **Stop Words**: No stop words (`the`, `a`, `an`, `of`) unless they add essential clarity.

### D. Heading Hierarchy
*   **H1 Rule**: Exactly **ONE `<h1>` per page** — matches the page's main topic and contains the primary keyword.
*   **Subheadings**: `<h2>`s for major sections, `<h3>`s for subsections.
*   **Hierarchy Law**: Never skip heading levels (e.g., no `<h1>` → `<h3>`).
*   **Meaningful Titles**: Headings describe what the section is about (never use generic titles like `"Section 1"`).

### E. Content Optimization & Structure
*   **Primary Keyword Placement**: First paragraph mentions the primary keyword naturally.
*   **Minimum Word Counts**:
    *   **Home Page**: 500 - 1,000 words.
    *   **Service Pages**: 800 - 1,500 words.
    *   **Blog Posts**: 1,500 - 3,000 words.
*   **Internal Linking**: Links to at least **2 to 3 other pages** using descriptive anchor text (e.g. `"our emergency plumbing services"` not `"click here"`).
*   **External Linking**: Includes links to authoritative external sources where relevant.
*   **Readability**: Short paragraphs (**2 to 4 sentences** maximum) and highly scannable structure.
*   **Search Intent**: Directly answers the search intent — what would someone searching this keyword want to know?

### F. Images
*   **Alt Text**: Descriptive `alt` text on every image, incorporating keywords naturally.
*   **Optimization**: Use framework-specific image components (e.g., Astro's `<Image>` or Next.js's `<Image>`) for automatic compression and optimization.
*   **Format**: Serve modern formats (WebP/AVIF) where possible.
*   **Layout Stability**: Specify appropriate width/height dimensions to prevent Cumulative Layout Shift (CLS).
*   **Loading Priorities**: Lazy load images residing below the fold (`loading="lazy"`).

### G. Structured Data
*   **JSON-LD Integration**: Every page gets at least one JSON-LD block.
*   **Validity Testing**: Ensure all scripts validate correctly using [Google's Rich Results Test](https://search.google.com/test/rich-results).

---

## 🏷️ 2. Production-Ready Structured Data Templates (JSON-LD)

To guarantee maximum rich snippet extraction, always embed structured schemas inside your layouts utilizing the standard `<script type="application/ld+json">` wrapper.

### A. WebSite Schema (Home Page Main Entry)
```json
{
  "@context": "https://schema.org",
  "@type": "WebSite",
  "name": "Business Name",
  "url": "https://yourdomain.com",
  "description": "Site description",
  "potentialAction": {
    "@type": "SearchAction",
    "target": "https://yourdomain.com/search?q={search_term_string}",
    "query-input": "required name=search_term_string"
  }
}
```

### B. LocalBusiness Schema (For Physical Locations)
```json
{
  "@context": "https://schema.org",
  "@type": "LocalBusiness",
  "name": "Business Name",
  "image": "https://yourdomain.com/logo.png",
  "url": "https://yourdomain.com",
  "telephone": "+353-1-234-5678",
  "address": {
    "@type": "PostalAddress",
    "streetAddress": "123 Main Street",
    "addressLocality": "Dublin",
    "addressRegion": "Dublin",
    "postalCode": "D01 AB12",
    "addressCountry": "IE"
  },
  "geo": {
    "@type": "GeoCoordinates",
    "latitude": 53.3498,
    "longitude": -6.2603
  },
  "openingHoursSpecification": [
    {
      "@type": "OpeningHoursSpecification",
      "dayOfWeek": ["Monday","Tuesday","Wednesday","Thursday","Friday"],
      "opens": "09:00",
      "closes": "17:30"
    }
  ],
  "priceRange": "$$"
}
```

### C. BlogPosting Schema (For Editorial Articles)
```json
{
  "@context": "https://schema.org",
  "@type": "BlogPosting",
  "headline": "Article Title",
  "description": "Article description",
  "image": "https://yourdomain.com/images/post.jpg",
  "datePublished": "2026-03-26T00:00:00Z",
  "dateModified": "2026-03-26T00:00:00Z",
  "author": {
    "@type": "Person",
    "name": "Author Name"
  },
  "publisher": {
    "@type": "Organization",
    "name": "Business Name",
    "logo": {
      "@type": "ImageObject",
      "url": "https://yourdomain.com/logo.png"
    }
  }
}
```

### D. FAQPage Schema (FAQ Sections — Great for Featured Snippets)
> [!WARNING]
> Google has restricted FAQPage rich result layouts for standard commercial e-commerce websites. Implement strictly on educational guides, authoritative info directories, or government routes.
```json
{
  "@context": "https://schema.org",
  "@type": "FAQPage",
  "mainEntity": [
    {
      "@type": "Question",
      "name": "What does your service cost?",
      "acceptedAnswer": {
        "@type": "Answer",
        "text": "Our services start from..."
      }
    }
  ]
}
```

### E. Service Schema (For Specific Business Offers)
```json
{
  "@context": "https://schema.org",
  "@type": "Service",
  "name": "Service Name",
  "description": "Service description",
  "provider": {
    "@type": "LocalBusiness",
    "name": "Business Name"
  },
  "areaServed": {
    "@type": "City",
    "name": "Dublin"
  },
  "serviceType": "Plumbing"
}
```

### F. BreadcrumbList Schema (Dynamic Navigation Traversal)
```json
{
  "@context": "https://schema.org",
  "@type": "BreadcrumbList",
  "itemListElement": [
    {
      "@type": "ListItem",
      "position": 1,
      "name": "Home",
      "item": "https://yourdomain.com"
    },
    {
      "@type": "ListItem",
      "position": 2,
      "name": "Services",
      "item": "https://yourdomain.com/services"
    }
  ]
}
```

---

## 📈 3. Content Optimization Rules

### A. Keyword Placement Priority
Always distribute primary and secondary target terms according to the following search-crawling priority:
1.  **Title tag**
2.  **H1 heading**
3.  **First 100 words of content** (First paragraph natural mention)
4.  **URL slug**
5.  **Meta description**
6.  **H2/H3 headings** (Secondary keywords)
7.  **Image alt text**
8.  **Internal link anchor text**

### B. Internal Linking Strategy
*   **Minimum Link Count**: Every page links to at least **2 to 3 other relevant pages** minimum.
*   **Descriptive Anchors**: Use descriptive anchor text: e.g. `"our emergency plumbing services"` not `"click here"` or `"read more"`.
*   **Pillar/Cluster Silos**: Blog posts link to relevant service pages (and vice versa) to transfer search engine equity.
*   **Navigation Architecture**: Navigation should surface your most important landing pages to ensure accessibility within a single click from the header.

### C. Local SEO Signals (For Local Businesses)
*   **Strict NAP Alignment**: Name, Address, and Phone (NAP) must be consistent on every page, usually in the global site footer.
*   **Geo Inclusion**: Include city/region names in titles and page content naturally.
*   **Local Landing Pages**: Create **"Areas We Serve"** pages if targeting multiple locations or municipal regions.
*   **LocalBusiness Schema**: Embed a LocalBusiness schema on every page.
*   **Google Maps Embed**: Embed Google Maps on the contact page to feed proximity signals to local engines.

---

## 🤖 4. Dec 2025 E-E-A-T & AI Engine Search (GEO)

### A. Core Update E-E-A-T Compliance (December 2025 Rules)
Google's December 2025 core update retired outdated ranking signals in favor of strict, experience-driven standards applied globally:
*   **First-Person Narrative Evidence**: Content must explicitly contain first-person proof points ("I tested...", "Our team physically ran...", "In my hands-on evaluation...").
*   **Original Visual Assets**: Include original graphics, charts, screenshots, or videos. Generic stock images are penalized.
*   **Explicit Bylines & Profiles**: Every informational guide must have a visible author byline linking directly to a dedicated profile bio detailing professional certifications, external authority profiles, and credentials.
*   **Really Simple Licensing (RSL 1.0)**: Deploy machine-readable licensing rules at the root level `/llms.txt` and domain files to dictate exactly how crawlers can utilize company content for LLM training vs search citations.

### B. Generative Engine Optimization (GEO) Standards
AI search platforms (Gemini, ChatGPT Search, Perplexity) select citation sources using entirely different extraction parameters:
*   **The Citability Sweet Spot**: AI engines extract answers best from self-contained passages of **134–167 words**.
*   **BLUF Definition Pattern**: Place direct answers or definitions in the first 40–60 words of an H2/H3 section using standard copula structures (e.g., *"X is a [definition] designed to resolve [problem]..."*).
*   **Speakable Specification Schema**: Embed CSS selector paths pointing directly to featured paragraphs within the page's JSON-LD script to assist voice engines:
    ```json
    {
      "@context": "https://schema.org",
      "@type": "WebPage",
      "speakable": {
        "@type": "SpeakableSpecification",
        "cssSelector": [".article-summary", "h2 + p", "#key-definition"]
      }
    }
    ```
*   **AI Crawler Management**: Configure `public/robots.txt` based on this technical standard:
    *   **Allow Indexing (Attributed Citations)**: Allow `OAI-SearchBot`, `PerplexityBot`, and `ClaudeBot` to scan public content.
    *   **Block Scrapers (Proprietary Shields)**: Deny bulk model training scrapers like `GPTBot`, `Claude-Web`, and `Google-Extended`.

---

## ⚡ 5. Technical SEO & Core Web Vitals Checks

### A. Core Web Vitals Optimization
*   **Image Optimization**: Use native framework components (like Astro's `<Image>` or Next.js's `<Image>`) for all images to enable automatic lazy loading and WebP/AVIF format conversion.
*   **Minimize JavaScript**: Minimize client-side JavaScript — use selective hydration (e.g., `client:visible` or lazy client imports) instead of loading all JS on page load (`client:load`) where possible.
*   **Inline Critical CSS**: Inline critical CSS (Astro and modern SSR bundlers do this automatically) to maximize rendering speeds.
*   **Link Prefetching**: Prefetch links for faster page navigation: `<link rel="prefetch" href="/about" />` or framework prefetch hooks.

### B. Canonical URLs
*   **Required Injections**: Every page must have a self-referencing canonical URL (the page points to itself) inside the raw server payload by default.
*   **Content Redundancy**: If content appears on multiple URLs, the canonical tag must point strictly to the preferred version.

### C. Sitemap
*   **Automation**: Sitemaps must be auto-generated by the framework plugins (e.g., `@astrojs/sitemap` or `next-sitemap`).
*   **Exclusions**: Exclude admin pages, API routes, database panels, and utility pages.
*   **Verification**: Verify sitemap outputs after build (check `dist/sitemap-index.xml` or target build folder).

### D. Robots.txt
*   **Exclusions**:
    *   **Allow**: All public routes and assets.
    *   **Disallow**: Block `/admin`, `/keystatic`, `/api/` dynamic endpoints, and database pages from search crawlers.
*   **Sitemap Integration**: Include the absolute XML sitemap URL pointer at the top or bottom of the `robots.txt` payload.
