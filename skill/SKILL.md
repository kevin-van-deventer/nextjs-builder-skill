---
name: nextjs-builder
description: "Build complete, SEO-optimized, and premium websites using Next.js 15+ App Router, React 19 Server Actions, Tailwind CSS, local Google fonts, and high-performance APIs. Use this skill whenever the user wants to create a Next.js website, improve their SEO, run pre-deploy audits, or build a fast local business landing page or e-commerce solution."
---

# Next.js Advanced Website Builder Skill

You build high-performance, dynamic, and deployment-ready websites in Next.js 15+ App Router that are engineered to rank on Google. Every project you build must strictly adhere to our modern UI/UX design tokens, state management, search engine optimization (SEO), and E-E-A-T playbook criteria.

Every frontend you produce must feel extremely premium, dynamic, and non-generic. Read the reference guidelines below before writing any code.

## References Directory

This skill is backed by specialized markdown guidelines which you can (and must) reference for precise technical specifications:
- `references/nextjs-instructions.md` — Core architectural rules for Next.js 15+ App Router, layout designs, and React 19 Server Actions.
- `references/best-practices.md` — UI/UX styling principles (HSL colors, glassmorphism, transitions, brand naming, project bootstrapping).
- `references/seo-and-eeat-playbook.md` — Google E-E-A-T compliance, GEO (Generative Engine Optimization), and structured data (JSON-LD) templates.
- `references/hosting.md` — Edge networks routing, Vercel caching, s-maxage headers, DNS canonicalization, and Netlify environments.
- `references/integrations.md` — Analytical tracking (Google Tag Manager) and dynamic Open Graph (OG) image generation utilizing React components.
- `references/pre-deploy-checklist.md` — Unified pre-deploy compilation check lists, Lighthouse score targets, and security validations.

---

## Technical Workflow Playbook

Always follow this chronological phased sequence when tasked with designing or building a web application:

### Phase 1: Niche Discovery & Content Research
1. Ask the user about their business niche, target audience, location, and visual styling preferences.
2. Ask if they need dynamic server storage/database capabilities (e.g. contact leads forms, reservation engines, dashboards).
3. Search the web to analyze ranking local competitors, high-equity search terms, and long-tail target keywords.
4. Propose a complete file-tree layout and custom page routing plan, requesting user approval prior to execution.

### Phase 2: Project Bootstrapping & Setup
Before generating visual layout code, initialize these metadata files at the project root to synchronize your roadmap:
1. **`todo.md`**: Organize the development phases in a living checklist (`- [ ]` status).
2. **`project-features.md`**: Create a detailed technical sheet outlining the technology stack, sitemap routing directory map, API integrations, and factual business contact variables.
3. **`brandkit.md`**: Define HSL color schemes (max 1 saturated accent color < 80%), dynamic transitions, and premium typography settings.
4. **Premium Typographies**: Configure and install high-end, premium localized Google Fonts (`next/font/google`) such as Outfit, Satoshi, Cabinet Grotesk, or Geist. **NEVER use browser defaults or generic Inter**.

### Phase 3: Modular Architecture & Database Setup
1. **Decouple Logic**: Strictly isolate functional logic (Authentication, database connections, schemas, React hooks, payment systems, GTM tags) from visual page shells.
2. **Directory Hygiene**: House reusable scripts inside dedicated `/components`, `/features`, `/services`, or `/lib` folders. Standalone page routes (`page.tsx`) must strictly import these blocks as structural templates.
3. **Database Integration**: If serverless database storage is needed, install ORM libraries (Drizzle ORM + Turso/LibSQL client). Define SQL table schemas for contact submissions, dynamic leads, or user registrations.
4. **Brand prefix styling**: All Tailwind color configurations in `tailwind.config.js` must be prefixed using the client's slugified business name (e.g., `moyres-gold`, `moyres-cream`), NEVER a generic `brand-` prefix.

### Phase 4: Core Implementation & Design Rules
1. **Layout & Grids**: Build out all visual page components. Avoid centered heroes or generic 3-column layouts; instead, leverage asymmetric, left-aligned, or split-screen grids.
2. **Responsive Bounds**: Enforce `min-h-[100dvh]` to prevent screen layout jumping on mobile dynamic address bars.
3. **Micro-Animations**: Configure smooth spring physics in interactive widgets (Framer Motion spring damping setups: stiffness 100, damping 20).
4. **Card Hierarchy**: Elevate card components only when conveying distinct content hierarchies. Avoid card borders and plain gray backgrounds.
5. **No AI Slop & Emojis**: Emojis, stock lorem-ipsum phrases, and placeholder data like "Acme Corp" or "John Doe" are **strictly forbidden**. Every copy block must be factual and highly researched.
6. **Heading Hierarchy**: Exactly one `<h1>` per page. Heading tags must be nested sequentially (H2s for sections, H3s for subsections) with no skipped levels. Natural primary keyword placement in the first paragraph of content (first 100 words).

### Phase 5: Technical SEO, GEO & Search Engine Compliance
1. **Protected Administrative Routing**: Create an administrative dashboard route `/admin` protected by a basic authentication middleware or Auth.js, rendering submitted leads and contact forms inside premium, styled tables.
2. **Sitemaps & Robots.txt**:
   - Configure compilations to auto-generate valid XML `sitemap.xml` index files, excluding administrative pages and backend API endpoints.
   - Set up a highly strategic `robots.txt` endpoint that:
     - Allows citation-equity search bots (`OAI-SearchBot`, `PerplexityBot`, `ClaudeBot`).
     - Disallows scraping models (`GPTBot`, `Claude-Web`, `Google-Extended`).
     - Excludes `/admin`, `/keystatic`, and `/api/` dynamic pathways.
     - Points directly to the absolute XML sitemap URL.
3. **Metadata & JSON-LD**: Inject server-side rendered canonical URLs and meta descriptions matching the targeted keywords inside dynamic `generateMetadata()`. Construct deep graph JSON-LD blocks combining WebSite, LocalBusiness, Service, or BlogPosting parameters.
4. **E-E-A-T Standards**: Incorporate first-person experiences ("our team evaluated", "in my hands-on test"), active author bylines linking to credential bios, and speakable schema CSS selectors.

### Phase 6: Edge Deployment & Caching Optimization
1. Implement Partial Prerendering (PPR) by wrapping dynamic leaf views in `<Suspense>` loaders, allowing static shell fragments to cache globally.
2. Configure edge caching HTTP headers (`s-maxage`) for static API endpoints, and establish clean CNAME and A-record settings in the domain manager.
3. Enforce 301 edge redirections within the Vercel dashboard, Cloudflare Pages rules, or `netlify.toml` to automatically redirect `www` variants to root canonical Apex domains.

### Phase 7: Quality Verification & Audit
1. Execute `npm run build` locally to detect any typescript errors, hydration shifts, or rendering conflicts.
2. View initial server-rendered HTML payloads via dry builds to guarantee metadata and JSON-LD validate correctly prior to client JavaScript execution.
3. Audit INP (< 200ms) and verify dynamic scripts utilize asynchronous Next.js `<Script>` components.
