---
name: "Next.js Integration Standards"
creator: "Kevin & Eduard"
version: "1.2.0"
last_updated: "2026-05-20"
description: "Framework-specific API connections, GTM tracking, dynamic OG card rendering, and connected graph JSON-LD Schemas in Next.js."
---

# 🔗 Next.js Technical Integration Standards

This playbook defines our standards for linking Next.js frontend applications to tracking dashboards, SEO graphs, and serverless communication APIs.

---

## 📈 1. Analytics & Tracking (@next/third-parties)

To prevent blocking the main rendering threads on dynamic App Router pages, we load Google tracking pixels using Next.js optimized built-in modules:

*   **Google Tag Manager (GTM)**: Install GTM on every client build using the official high-performance GTM wrapper:
    ```tsx
    import { GoogleTagManager } from '@next/third-parties/google'

    export default function RootLayout({ children }: { children: React.ReactNode }) {
      return (
        <html lang="en">
          <body>
            {children}
            <GoogleTagManager gtmId={process.env.NEXT_PUBLIC_GTM_ID || ''} />
          </body>
        </html>
      )
    }
    ```
*   **Event Verification**: Verify dynamic event triggers (such as e-commerce clicks or telephone clicks) using GTM Preview Mode before pushing changes to staging.

---

## 🎨 2. Dynamic Open Graph (OG) Images (ImageResponse)

Next.js supports native, dynamic open-graph image generation directly in your code using JSX and CSS:

*   **File Location**: Build your generator script inside the route folder under `src/app/opengraph-image.tsx` (or `app/[slug]/opengraph-image.tsx` for dynamic product listings).
*   **Implementation Blueprint**:
    ```tsx
    import { ImageResponse } from 'next/og'

    export const alt = 'Unlimited Solutions Enterprise'
    export const size = { width: 1200, height: 630 }
    export const contentType = 'image/png'

    export default async function Image() {
      return new ImageResponse(
        (
          <div
            style={{
              background: '#090d16',
              width: '100%',
              height: '100%',
              display: 'flex',
              flexDirection: 'column',
              alignItems: 'center',
              justifyContent: 'center',
              fontFamily: 'sans-serif'
            }}
          >
            {/* Soft Aurora Mesh Background */}
            <div
              style={{
                position: 'absolute',
                top: '-150px',
                left: '-150px',
                width: '600px',
                height: '600px',
                background: 'radial-gradient(circle, rgba(59, 130, 246, 0.15) 0%, rgba(9, 13, 22, 0) 70%)',
                borderRadius: '50%'
              }}
            />
            
            <h1
              style={{
                color: '#3b82f6',
                fontSize: 64,
                fontWeight: 'bold',
                margin: 0,
                letterSpacing: '-0.02em'
              }}
            >
              Unlimited Solutions
            </h1>
            <p
              style={{
                color: '#94a3b8',
                fontSize: 24,
                marginTop: 16,
                letterSpacing: '0.05em',
                textTransform: 'uppercase'
              }}
            >
              High-Performance Edge Architecture
            </p>
          </div>
        ),
        { ...size }
      )
    }
    ```

---

## 🤖 3. E-E-A-T Connected Graph Schemas (JSON-LD)

To provide search engine crawlers with semantic data, we construct deep, connected JSON-LD graphs linking website author, business, and tech stack details:

*   **Implementation**: Inject a `@graph` JSON script inside your page components:
    ```tsx
    export default function Page() {
      const jsonLd = {
        "@context": "https://schema.org",
        "@graph": [
          {
            "@type": "WebSite",
            "@id": "https://domain.com/#website",
            "url": "https://domain.com",
            "name": "Steel Saigon",
            "publisher": { "@id": "https://domain.com/#developer" }
          },
          {
            "@type": "Person",
            "@id": "https://domain.com/#developer",
            "name": "Kevin v Dev",
            "jobTitle": "Full-Stack Software Engineer",
            "knowsAbout": ["React", "Next.js", "Serverless Edge", "Technical SEO"]
          }
        ]
      }

      return (
        <script
          type="application/ld+json"
          dangerouslySetInnerHTML={{ __html: JSON.stringify(jsonLd) }}
        />
      )
    }
    ```
*   **Verification**: Always test JSON-LD schemas using the [Schema Markup Validator](https://validator.schema.org/) before deployments.
