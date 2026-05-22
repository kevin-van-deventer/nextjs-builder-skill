---
name: "Prompt Engineering & System Design Best Practices"
creator: "Kevin & Eduard"
version: "1.2.0"
last_updated: "2026-05-20"
description: "Guidelines and blueprints for creating elite prompt architectures and micro-interactions."
---

# 💡 Prompt Engineering & System Design Best Practices

This document contains our shared engineering principles, design systems, and prompt styling recommendations. As we learn more from LLM behaviors, we will update this document to keep our standards state-of-the-art.

---

## 🎨 1. UI/UX & Styling Standards

When designing web applications, all system prompts and agents must be instructed to default to these principles:

### 🌈 HSL Color Harmonies
*   Do **NOT** use hardcoded, generic colors (e.g. `red`, `blue`, `#ff0000`).
*   Always use HSL variables in CSS to define modern, adjustable themes:
    ```css
    :root {
      --primary-hsl: 220 90% 56%;    /* Sleek Electric Blue */
      --background-hsl: 222 47% 11%; /* Premium Deep Navy */
      --foreground-hsl: 210 40% 98%;
      --card-hsl: 224 71% 4%;
      --border-hsl: 217 19% 27%;
    }
    ```

### ❄️ Glassmorphism
*   Implement elegant glassy interfaces using backdrop-filters:
    ```css
    .glass-panel {
      background: rgba(15, 23, 42, 0.45);
      backdrop-filter: blur(12px);
      -webkit-backdrop-filter: blur(12px);
      border: 1px solid rgba(255, 255, 255, 0.08);
      border-radius: 16px;
    }
    ```

### 🏎️ Transitions & Micro-interactions
*   Ensure buttons, links, and cards feel responsive and alive:
    ```css
    .interactive-element {
      transition: all 0.3s cubic-bezier(0.4, 0, 0.2, 1);
    }
    .interactive-element:hover {
      transform: translateY(-2px) scale(1.02);
      box-shadow: 0 10px 20px rgba(0, 0, 0, 0.2);
    }
    ```

### 🏷️ Brand Class Naming Conventions
*   All Tailwind CSS color utility classes must be **prefixed with the business or project name**, never a generic `brand-` prefix.
*   This ensures each project's design system is semantically tied to the client's identity, avoids style conflicts between multiple client projects, and makes code instantly recognizable in multi-project workspaces.
*   **Rule:** When generating or configuring a `tailwind.config.js` color palette, the color group key must be the **slugified business name** (lowercase, no spaces), and each utility class must follow the format `{business-name}-{color-role}`.
*   **DO NOT use:** `bg-brand-gold`, `text-brand-forest`, `border-brand-cream`
*   **ALWAYS use:** `bg-{business}-gold`, `text-{business}-forest`, `border-{business}-cream`

    ```js
    // ✅ CORRECT – Moyres Site example
    module.exports = {
      theme: {
        extend: {
          colors: {
            moyres: {
              forest: "hsl(var(--primary-forest) / <alpha-value>)",
              cream:  "hsl(var(--secondary-cream) / <alpha-value>)",
              gold:   "hsl(var(--accent-gold) / <alpha-value>)",
            }
          }
        }
      }
    }

    // ❌ INCORRECT – Generic prefix, not allowed
    module.exports = {
      theme: {
        extend: {
          colors: {
            brand: {
              forest: "hsl(var(--primary-forest) / <alpha-value>)",
              // ...
            }
          }
        }
      }
    }
    ```

*   This convention applies to **all utility class variants**, including:
    *   Background colors: `bg-moyres-gold`, `bg-moyres-forest/10`
    *   Text colors: `text-moyres-charcoal`, `text-moyres-cream/80`
    *   Border colors: `border-moyres-sage`, `border-moyres-forest/20`
    *   Gradient stops: `from-moyres-forest`, `via-moyres-gold`, `to-moyres-cream`
    *   Hover/focus variants: `hover:bg-moyres-gold`, `focus:ring-moyres-forest`
    *   Selection utilities: `selection:bg-moyres-forest/10`
    *   Shadow colors: `shadow-moyres-forest/20`

---

## ✍️ 2. Writing Elite Prompts (System Design Guide)

To write instructions that LLMs follow reliably, utilize these high-performance prompt engineering methodologies:

### 🎭 A. Role & Attention Contextualization
Always establish the role and specialized credentials of the agent at the absolute beginning of the instructions. The model needs a high-weight semantic vector to anchor its attention mechanism:
- **Poor**: *"You are a coder. Help me fix my code."*
- **Elite**: *"You are an elite, performance-focused React compiler agent and Senior Frontend Architect specializing in JSX rendering optimization."*

### 🏷️ B. XML-Tagged Instruction Structuring
Use XML tags to isolate variables, boundaries, context, and operational steps. LLMs are trained heavily on structural markup, making XML-tagged blocks highly effective at minimizing instruction-drift:
```markdown
<context>
You are tasked with reviewing client portfolios for styling layout shifts.
</context>

<constraints>
- Never use inline styles.
- Only suggest HSL color scales.
</constraints>

<instructions>
1. Parse the inputted CSS rules.
2. Identify border transformations causing layout shifts.
3. Suggest hardware-accelerated replacements.
</instructions>
```

### 🧠 C. Mandating Chain-of-Thought (CoT)
For complex logical tasks (debugging, architecture, design-system planning), instruct the model to perform a verbose mental analysis inside a dedicated `<thinking>` block *prior* to rendering the final output. This forces the model's auto-regressive decoding to map out path solutions:
```markdown
You must structure your response using the layout below:

<thinking>
[Perform a deep, step-by-step analysis of the problem, verifying all constraints]
</thinking>

[Your actual, production-ready solution goes here]
```

### 🚫 D. Negative Constraints & Absolute Boundaries
LLMs are highly responsive to explicit exclusions. Clearly isolate what the model **must NOT do**:
- *"Never use stock images or placeholders. If an image is required, describe it in detail or use exact URLs."*
- *"Do not write incomplete code blocks, mock functions, or leave comments like `// TODO: Implement later`."*

### 📚 E. Few-Shot Prompting Schemas
For complex formatting requirements, supply the model with at least one high-fidelity input/output pairing to demonstrate the exact expected behavior:
```markdown
### 📥 Example Input:
User wants to color a card border electric blue.

### 📤 Example Output:
```css
border: 1px solid hsl(220, 90%, 56%);
```
```

---

## 🏗️ 3. Core Software Engineering Standards

### Architectural Rule: Component Modularity & Reusability

To ensure the application can be easily redeveloped or redesigned in the future, all functional business logic must be strictly decoupled from visual page layouts and routing files.

* **Isolate Core Logic:** All functional features must be built as self-contained, modular pieces. This applies to:
  * **Authentication & Authorization** (Login flows, protected routes, session handling)
  * **Database Interactions** (Queries, mutations, ORM configurations, data models)
  * **API Integrations & Services** (Fetch/Axios setups, external API clients)
  * **Forms & Validation** (Input handling, multi-step forms, schema validations)
  * **Middleware & Gatekeepers** (Request parsing, security headers, logging, edge functions)
  * **State Management** (Global stores, custom hooks, context providers)
  * **Third-Party Services** (Payment gateways, webhooks, analytics, tracking scripts)
* **Directory Structure:** These components, hooks, utilities, and middleware must reside in dedicated, organized folders (e.g., `/components`, `/features`, `/middleware`, `/services`). They must never be hardcoded into standalone page views.
* **Design Independence:** Page-level files should act strictly as layout templates and routers. They must import these functional blocks. This guarantees that if the visual design changes or the front-end framework is redeveloped, the core application logic remains completely intact and instantly reusable.

### Project Initialization & Asset Bootstrapping Rule

To ensure every new workspace is structured consistently and has clear operational goals and visual identities from day one, all new projects must strictly adhere to the following bootstrapping protocols:

*   **Mandatory `todo.md` Creation:** Immediately upon starting a new project, you must create a `todo.md` file at the project root. This file serves as the single source of truth for the project roadmap, listing all technical features, business requirements, and operational integrations needed (e.g., Google Authentication, database systems for user records, Google Maps API business locations, payment processing, form-submission endpoints, etc.). Tasks must be organized into phased milestones (e.g., Phase 1: Core Launch, Phase 2: SEO, Phase 3: Integrations) and tracked with checkbox status markers (`- [ ]` uncompleted, `- [x]` complete).
*   **Mandatory `project-features.md` Creation:** Every new project must also include a `project-features.md` file at the project root. This document is the **technical specification sheet** for the project and must be created before any architecture decisions or coding begins. It must cover:
    *   **Framework & Technology Stack**: The chosen framework (Next.js, Astro, etc.), language (TypeScript/JavaScript), styling system (Tailwind CSS + brand token prefix), hosting provider (Cloudflare Pages, Vercel, etc.), and package manager.
    *   **Routing Architecture**: A file-tree diagram mapping all planned URL routes and their corresponding page components.
    *   **Core Features**: A descriptive list of the primary functional features to build (e.g., dual-site architecture, live booking engine, inquiry form, gallery).
    *   **Third-Party API Integrations**: A table listing every external service, its purpose, and its integration status (e.g., Google Maps, Stripe, Resend, GTM, GA4, Meta Pixel, WhatsApp Business).
    *   **Design System Reference**: A pointer to the `brandkit.md` file, the brand color token prefix, and the font selections.
    *   **Business Information**: Client contact details, physical address, GPS coordinates, and any other factual data the agent will need when generating copy or schemas.
*   **Mandatory `brandkit.md` Initialization:** Every project must start with a cohesive visual design system defined in a `brandkit.md` file at the root. Prior to writing any UI components, the brand kit must be established by either:
    *   **Manual Creation:** The user or developer manually authoring and adding a `brandkit.md` detailing CSS theme variables, HSL color schemes, logo assets, typography settings, and UI component designs.
    *   **AI/Agent Generation:** Invoking an Antigravity agent model (e.g., Gemini) to dynamically design and generate a custom `brandkit.md` based on the client's business niche, aesthetic preferences, and industry design standards.

### Workspace Hygiene & Git Exclusion Rule

To prevent repository bloat, accidental security exposure, and deployment payload inflation, the project workspace must enforce strict asset exclusion policies:

*   **Excluding Non-Production Markdown:** All operational instruction manuals, prompts, playbooks, templates, and agent documentation (`best-practices.md`, guidelines, template files) that reside outside the production website folder structure must be added to the project's `.gitignore` file.
*   **Excluding Agentic Clutter:** All temporary assets created during agent reasoning or execution—such as debugging screenshots (`.png`, `.jpg`, `.webp`), logs, scraped page assets, and test dumps—must be ignored in `.gitignore`.
*   **Production Parity:** Ensure only files and folders strictly necessary for building, compiling, and running the web application (e.g., source code, lockfiles, configuration files, and verified static assets) are tracked by Git.

---
© 2026 FullWebDevKev · Crafted with ★
