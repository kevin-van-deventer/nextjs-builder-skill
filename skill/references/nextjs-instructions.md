---
name: "Next.js Instructions & Checklists"
creator: "Kevin & Eduard"
version: "1.2.0"
last_updated: "2026-05-20"
description: "Framework-specific performance constraints, SEO checklists, and server-side parity rules for Next.js 15+ App Router."
---

# 🚀 Next.js SEO & Performance Master Checklist

This document contains our strict developer guidelines, SEO requirements, and build optimization checklists when creating high-end Next.js App Router projects.

---

## 🏗️ 1. Core Architecture (Next.js 15 & React 19 Standards)

*   **Next.js 15+ (App Router)**: Always leverage the App Router standard for all new dynamic platforms.
*   **React 19 Server Actions**: Restrict data-mutations to async Server Actions (`'use server'`). Wrap server-action submissions in the new React 19 `useActionState` hook inside form components to manage loading, validation errors, and success states natively without client state libraries.
*   **layout.tsx Shared Assets**: Declare central layout components, shared headers, and global metadata inheritance inside `/app/layout.tsx`.
*   **metadataBase**: Setup the global `metadataBase` utilizing our `NEXT_PUBLIC_SITE_URL` env variable in the top-level layout to guarantee canonical URLs resolve correctly.
*   **Environment Keys**: Prefix client-facing keys with `NEXT_PUBLIC_` inside `.env.local` to allow client-side hydration.
*   **Component Modularity & Reusability**: Decouple functional business logic (Auth, DB interactions, APIs, forms validation, custom hooks, and third-party scripts) from page-level layouts and routing files. Standalone pages (`page.tsx`) should act strictly as structural layout templates that import modular components and hooks. This guarantees that if the visual design changes, the core application logic remains intact and reusable.
*   **Project Bootstrapping SOP**: Immediately upon starting a new project, initialize a root-level `todo.md` listing all required technical features organized into phased milestones (e.g., Phase 1: Core Launch, Phase 2: SEO, Phase 3: Integrations). Also create a `project-features.md` at the root — the **technical specification sheet** — covering the framework/tech stack, routing architecture file-tree, core feature descriptions, third-party API integrations table (Google Maps, Stripe, Resend, GTM, GA4, etc.), design system reference, and full client business information. Additionally, establish a `brandkit.md` file at the root — either manually created or generated using Antigravity agent models (e.g., Gemini) — to ensure theme and style parameters are defined before building or styling components.
*   **Brand Class Naming Convention**: When configuring the Tailwind `colors` section in `tailwind.config.js`, the color group key **must be the slugified business name** (e.g., `moyres`, `acme`, `shopify`), never the generic `brand` keyword. All utility classes in components and pages must follow `{business}-{color-role}` (e.g., `bg-moyres-gold`, `text-moyres-forest`, `border-moyres-cream`). Generic `brand-` prefixed classes are strictly prohibited.
*   **Workspace Hygiene & Git Exclusion**: Ensure that all operational instructions, agent prompt guidelines, and templates outside the website's app folder are excluded via `.gitignore`. Additionally, exclude any agentic screenshots, diagnostic scrapings, and debug logs to keep the repository clear of bloat.

---

## ⚡ 2. Edge Performance & PPR (Partial Prerendering)

*   **Suspense Boundaries**: Wrap dynamic database entries, session verification cards, and user carts inside React `<Suspense>` components to enable **Partial Prerendering (PPR)**. This ensures that Vercel edge networks can instantly cache and render the static visual page frame (improving LCP) while asynchronously streaming dynamic widgets.
*   **next/image Rules**:
    *   **sizes Attribute**: **MANDATORY**. Define explicit `sizes` parameters on all `<Image>` elements to prevent downloading full-res assets on mobile.
    *   **priority Hero**: Add the `priority` attribute to the above-the-fold Hero banner image to prevent render blocking.
*   **next/font self-hosting**: Host Google Fonts locally using `next/font/google` to eliminate FOIT (Flash of Invisible Text) and render delays.

---

## 🌐 3. Server-Rendered Parity & JavaScript SEO (Google Dec 2025)

Google's advanced rendering rules mandate absolute consistency between initial raw server responses and client-side hydrated trees:
*   **Canonical Parity**: Enforce that canonical tags are served directly inside the initial server-side rendered HTML response (using Next.js `generateMetadata()` or global layout config). Never rely on client-side React hydration or hooks to overwrite canonical links, as conflicts will result in indexing penalties.
*   **Server-Side robots noindex**: If a route is private or requires exclusion, serve the `<meta name="robots" content="noindex">` tag in the initial server payload. Never rely on client-side code or JS hydration to dynamically insert or remove robots directives—Googlebot may crawl the initial server-side payload and cache the noindex forever.
*   **Time-Sensitive Structured Data**: Product price, availability, and Article metadata schemas must be completely server-rendered. Dynamic injection via client hydration risks delayed processing by Google's indexers.
*   **Static Error Pages**: Ensure Next.js custom pages (e.g., `/app/not-found.tsx` or dynamic error boundaries) compile critical HTML structures server-side. Googlebot **does not execute JavaScript** on pages returning non-200 HTTP status codes, meaning any hydrated links or text will be invisible.

---

## 🧪 4. Production Validation Checklist

*   [ ] **Lighthouse Mobile Score**: Target a mobile and desktop performance rating of **90+**.
*   [ ] **Build-time Compiles**: Always run `npm run build` -> `npm run start` to execute audits on a true production bundle, verifying there are zero hydration mismatches.
*   [ ] **Initial Render Audit**: View the raw source HTML (e.g. via `curl` or browser View Source) to guarantee that all meta headers, structured JSON-LD schemas, and canonical tags exist prior to JavaScript execution.
*   [ ] **Third-party tag loading**: Verify dynamic scripts are loaded asynchronously utilizing the Next.js `<Script>` optimization component.
