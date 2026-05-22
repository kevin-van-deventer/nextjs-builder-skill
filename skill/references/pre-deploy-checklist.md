---
name: "Next.js Pre-Deploy Checklist"
creator: "Kevin & Eduard"
version: "1.0.0"
last_updated: "2026-05-20"
description: "Comprehensive verification checklist for deploying Next.js 15 App Router applications onto Vercel and Netlify."
---

# 🚀 Next.js Pre-Deploy Verification Checklist

Run through this systematic checklist before executing any production deployments of Next.js applications onto **Vercel** or **Netlify** edge platforms.

---

## ⚡ 1. Framework-Specific Compilations (Next.js 15 & React 19)

### 📦 A. Static & Dynamic Build Health
*   [ ] **Build Verification**: Run `npm run build` locally. Verify that the build completes without TypeScript compilation errors or ESM/CommonJS import anomalies.
*   [ ] **Server Action Types**: Ensure all server-side functions executed inside form handlers are explicitly declared with the `"use server"` string directive at the top of the file.
*   [ ] **Async Parameters (Next.js 15 Rule)**: Check that dynamic URL params and searchParams parameters inside layout/page paths are handled as promises and explicitly awaited:
    ```typescript
    interface Props {
      params: Promise<{ id: string }>;
    }
    export async function Page({ params }: Props) {
      const { id } = await params; // MANDATORY in Next.js 15
    }
    ```
*   [ ] **Hydration Splitting**: Validate that all client hook components (`useState`, `useEffect`, React 19 `useActionState`) are partitioned into leaf components marked with `'use client'`. Server-side components must act as the primary structural parents.
*   [ ] **Suspense PPR Boundaries**: Verify that all dynamic widgets fetching live data or sessions are wrapped inside React `<Suspense>` boundaries to guarantee the static shell loads instantly.

### 🔍 B. On-Page & Technical SEO Verification
*   [ ] **Unique Title Tags**: Confirm every route has a unique title tag under 60 characters, with the primary keyword near the start, in format `"Primary Keyword | Brand Name"`, designed as a compelling headline.
*   [ ] **Unique Meta Descriptions**: Confirm meta descriptions are under 160 characters, contains primary keyword, and includes a clear call-to-action (CTA) to maximize CTR.
*   [ ] **URL Slug Formats**: Verify URL slugs are short, lowercase, contain target keyword, separated by hyphens (no underscores), with zero stop words unless essential.
*   [ ] **Heading Hierarchy Law**: Ensure exactly ONE `<h1>` per page matching the page topic and containing the primary keyword. All subheadings (`<h2>`, `<h3>`) must nest sequentially (no skipping levels like `<h1>` → `<h3>`), and contain descriptive text (avoid `"Section 1"`).
*   [ ] **First-Paragraph Keyword**: Verify primary keyword is placed naturally within the first paragraph of content (first 100 words).
*   [ ] **Content Length Standards**: Confirm minimum word counts are met: Home (500 - 1,000), Service pages (800 - 1,500), Blog posts (1,500 - 3,000).
*   [ ] **Linking Strategies**: Verify each page has a minimum of 2-3 internal links using highly descriptive anchor texts (e.g., `"our emergency plumbing services"`, never `"click here"`), and includes authoritative external outbound links where relevant.
*   [ ] **JSON-LD Schema Integration**: Validate that every route has a valid, server-rendered JSON-LD block using standard `<script type="application/ld+json">` configurations matching workspace Dublin boilerplates.
*   [ ] **No Commercial FAQ Schemas**: Ensure FAQPage/HowTo schemas are strictly restricted to info/edu/gov pages and never deployed on standard commercial platforms.
*   [ ] **Dynamic Metadata**: Ensure `generateMetadata()` is implemented on all dynamic routes (e.g. blog posts, product pages) to programmatically serve correct titles, descriptions, and canonical URLs.
*   [ ] **Self-Referenced Canonicals**: Confirm canonical URL elements point strictly to primary production addresses inside the raw server payload, eliminating staging URLs.
*   [ ] **Open Graph Dimensions**: Ensure that OG sharing card images are linked, exist on the server, and measure the standard **1200 $\times$ 630px** size.
*   [ ] **Sitemap & Robots Check**: Verify that `next-sitemap` or native Next.js sitemap hooks compile standard `sitemap.xml` and `robots.txt` output schemas to the root `/public` or `/app` directory. Ensure `robots.txt` whitelists attributed AI bots (`OAI-SearchBot`, `PerplexityBot`, `ClaudeBot`) and disallows scrapers (`GPTBot`, `Claude-Web`, `Google-Extended`).

### 🚀 C. CWV & Loading Speed Checks
*   [ ] **Image Sizing (`next/image`)**: Ensure all images use the native `<Image>` component with dynamic `sizes` parameters and absolute width/height dimensions to prevent serving desktop assets to mobile layouts and eliminate CLS.
*   [ ] **Above-the-Fold Priority**: Confirm the main hero graphic has `priority={true}` configured to maximize Largest Contentful Paint (LCP) times.
*   [ ] **Link Prefetching**: Confirm high-priority page links utilize Next.js prefetching parameters or `<link rel="prefetch" />` tags to enable instantaneous client navigation.
*   [ ] **Self-Hosted Typography**: Verify that Google Fonts are hosted locally using `next/font/google` to eliminate FOIT layout shifts.
*   [ ] **No FID References**: Ensure all speed logs focus on **INP < 200ms** and do not reference the retired First Input Delay (FID) metric.

### 🛡️ D. Security & Data Protection
*   [ ] **Gitignore Compliance**: Check that `.env` and `.env.local` are listed inside `.gitignore`.
*   [ ] **API Secret Isolation**: Ensure no private backend tokens or database credential variables are prefixed with `NEXT_PUBLIC_`, keeping them securely isolated to the server.
*   [ ] **Input Validation Bounds**: Ensure all API routes parse payload inputs through strict **Zod** schema checkers.
*   [ ] **Admin Routings**: Enforce middleware checking for administrative JWTs or session tokens before compiling admin views.

---

## 🚢 2. Platform-Specific Deployment Configurations

Select the checklist matching your target production edge provider:

### 📐 Track A: Vercel Deployments
*   [ ] **Primary Domain redirection**: In **Project Settings > Domains**, confirm that `www.domain.com` is configured to redirect to the canonical root `domain.com` (or vice-versa) at the edge.
*   [ ] **Speed Insights Active**: Check that **Vercel Speed Insights** is enabled in the hosting dashboard to collect real-user core web vitals.
*   [ ] **Deployment Protection Credentials**: For active staging branches, verify that password protection is enabled to prevent search engine scrapers from indexing unfinished pages.
*   [ ] **ISR Caching Schedules**: Check that `export const revalidate` values on dynamic routes are properly timed to prevent high database compute costs.
*   [ ] **Edge Config variables**: Ensure any feature flags or maintenance settings are correctly populated inside the Vercel Edge Config key-value panel.
*   [ ] **Secure Environment Sync**: Verify all production API credentials match local values in Vercel's environment settings dashboard.

### ⚡ Track B: Netlify Deployments
*   [ ] **Build & Publish Directory**: Ensure Netlify's build parameters match Next.js App Router rules:
    *   **Build command**: `npm run build`
    *   **Publish directory**: `.next`
*   [ ] **Netlify Runtime Plugin**: Confirm that Netlify's Next.js Runtime plugin is active to allow serverless routing and dynamic rendering to execute smoothly.
*   [ ] **netlify.toml Routing**: Verify the root `netlify.toml` configuration contains the canonical WWW-to-Apex redirect rule:
    ```toml
    [[redirects]]
      from = "https://www.yourdomain.com/*"
      to = "https://yourdomain.com/:splat"
      status = 301
      force = true
    ```
*   [ ] **Asset Caching Headers**: Ensure standard asset routing caching is declared for `/_next/static/*` assets with `max-age=31536000, immutable`.
*   [ ] **Secure Header Declarations**: Verify standard security headers (CSP, HSTS, X-Content-Type-Options) are compiled inside `netlify.toml`.
*   [ ] **Staging Crawler Protections**: Configure Netlify Site Password protections on staging URLs to block search crawler indexation.
