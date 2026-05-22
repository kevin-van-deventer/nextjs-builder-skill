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

### Phase 2: Project Bootstrapping
Before generating visual layout code, initialize these metadata files at the project root to synchronize your roadmap:
1. **`todo.md`**: Organize the development phases in a living checklist (`- [ ]` status).
2. **`project-features.md`**: Create a detailed technical sheet outlining the technology stack, sitemap routing directory map, API integrations, and factual business contact variables.
3. **`brandkit.md`**: Define CSS custom properties, HSL color schemes, dynamic transitions, and typography settings.

### Phase 3: Modular Architecture Setup
1. **Decouple Logic**: Strictly isolate functional logic (Authentication, database connections, schemas, React hooks, payment systems, analytics tags) from visual page shells.
2. **Directory Hygiene**: House reusable scripts inside dedicated `/components`, `/features`, `/services`, or `/lib` folders. Standalone page routes (`page.tsx`) must strictly import these blocks as structural templates.
3. **Brand prefix styling**: All Tailwind color configurations in `tailwind.config.js` must be prefixed using the client's slugified business name (e.g., `moyres-gold`, `moyres-cream`), NEVER a generic `brand-` prefix.

### Phase 4: Core Implementation & Content Building
1. Build out all visual page components utilizing the Tailwind custom brand utility styles.
2. Write original, fully-researched content. Emojis, stock lorem-ipsum phrases, and placeholder data like "Acme Corp" or "John Doe" are **strictly forbidden**.
3. Incorporate strict Heading Hierarchy (exactly one `<h1>` per page, nested subheadings without level-skipping, and natural primary keyword inclusion in the first 100 words of copy).
4. Utilize localized Google Fonts (`next/font/google`) to prevent FOIT, and configure native `<Image>` components with mandatory responsive `sizes` values to maximize LCP speeds.

### Phase 5: Technical SEO, GEO & E-E-A-T Compliance
1. Inject server-side rendered canonical URLs and dynamic meta descriptions matching the targeted keywords inside dynamic `generateMetadata()`.
2. Construct deep, connected graph JSON-LD blocks combining WebSite, LocalBusiness, Service, or BlogPosting parameters.
3. Align search content to Dec 2025 E-E-A-T core standards: incorporate first-person narrative experiences ("our team evaluated", "in my hands-on test"), active author bylines linking to credential bios, and speakable schema CSS selectors.
4. Set up `/llms.txt` and robots.txt settings to authorize indexable citations while block-restricting bulk proprietary scrapers.

### Phase 6: Edge Deployment & Caching Optimization
1. Implement Partial Prerendering (PPR) by wrapping dynamic leaf views in `<Suspense>` loaders, allowing static shell fragments to cache globally.
2. Configure edge caching HTTP headers (`s-maxage`) for static API endpoints, and establish clean CNAME and A-record settings in the domain manager.
3. Enforce 301 edge redirections within the Vercel dashboard or `netlify.toml` to automatically redirect `www` variants to root canonical Apex domains.

### Phase 7: Quality Verification & Audit
1. Execute `npm run build` locally to detect any typescript errors, hydration shifts, or rendering conflicts.
2. View initial server-rendered HTML payloads via dry builds to guarantee metadata and JSON-LD validate correctly prior to client JavaScript execution.
3. Audit INP (< 200ms) and verify dynamic scripts utilize asynchronous Next.js `<Script>` components.
