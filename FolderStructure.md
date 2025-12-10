# Popverse – Folder Structure Specification

## 1. Purpose

This document defines the **recommended Next.js (App Router) folder structure** for the Popverse project. The goal is to:

* Keep the project scalable and maintainable
* Avoid moving files between folders in the future
* Clearly separate UI, business logic, data access, and configuration

---

## 2. High-Level Project Layout

```text
popverse/
├── src/
│   ├── app/
│   ├── components/
│   ├── lib/
│   ├── models/
│   ├── hooks/
│   ├── types/
│   ├── config/
│   ├── styles/
│   ├── learning/
│   └── middleware.ts
├── public/
├── scripts/
├── .env.*
└── package.json
```

**Notes:**

* All main code lives under `src/`.
* `app/` handles routing and layouts.
* Reusable logic and structures are separated into `components/`, `lib/`, `models/`, `hooks/`, `types/`, and `config/`.

* `learning/` is a developer-facing folder for short, incremental notes you create while building (commands, pitfalls, migration steps). Keep one topic per file and link them from `src/learning/notes.md`.

---

## 3. `src/app` – Routes & Layouts

```text
src/app/
├── layout.tsx                 # Root layout (Navbar, Footer, theme)
├── page.tsx                   # Public Home page
├── about/
│   └── page.tsx
├── login/
│   └── page.tsx
├── signup/
│   └── page.tsx
├── [category]/
│   ├── page.tsx               # Category listing page
│   └── [slug]/
│       └── page.tsx           # Article detail page
├── tags/
│   └── [slug]/
│       └── page.tsx
├── search/
│   └── page.tsx
├── admin/
│   ├── layout.tsx             # Admin layout (sidebar, header)
│   ├── dashboard/
│   │   └── page.tsx
│   ├── articles/
│   │   ├── page.tsx           # List
│   │   ├── create/
│   │   │   └── page.tsx
│   │   └── [id]/
│   │       └── page.tsx       # Edit
│   ├── comments/
│   │   └── page.tsx
│   ├── categories/
│   │   └── page.tsx
│   ├── tags/
│   │   └── page.tsx
│   ├── ads/
│   │   └── page.tsx
│   ├── users/
│   │   └── page.tsx
│   └── analytics/
│       └── page.tsx
└── api/
    ├── auth/
    │   ├── login/route.ts
    │   ├── signup/route.ts
    │   └── me/route.ts
    ├── articles/
    │   ├── route.ts           # List + create
    │   └── [id]/route.ts      # Get + update + delete
    ├── comments/
    │   └── [articleId]/route.ts
    ├── categories/
    │   └── route.ts
    ├── tags/
    │   └── route.ts
    ├── ads/
    │   └── route.ts
    └── analytics/
        └── views/route.ts
```

**Key Ideas:**

* Public routes and admin routes live side-by-side but separated by folder.
* API routes are grouped by resource (articles, comments, tags, etc.).
* URLs match the SEO structure defined in the main SRS.

---

## 4. `src/components` – Reusable UI

```text
src/components/
├── ui/                        # shadcn/ui components
├── layout/
│   ├── navbar.tsx
│   ├── footer.tsx
│   ├── admin-sidebar.tsx
│   └── language-switcher.tsx
├── common/
│   ├── logo.tsx
│   ├── search-input.tsx
│   ├── pagination.tsx
│   ├── loading-spinner.tsx
│   └── empty-state.tsx
├── article/
│   ├── article-card.tsx
│   ├── article-list.tsx
│   ├── article-header.tsx
│   ├── article-meta.tsx
│   ├── article-content.tsx
│   └── related-articles.tsx
├── comments/
│   ├── comment-list.tsx
│   ├── comment-item.tsx
│   └── comment-form.tsx
├── ads/
│   └── ad-slot.tsx
└── analytics/
    └── stats-card.tsx
```

**Guidelines:**

* `layout/` → components that appear globally (Navbar, Footer, etc.).
* `article/`, `comments/`, `ads/`, `analytics/` → grouped by feature.
* Keep components **presentational**; business logic goes to hooks/lib.

---

## 5. `src/lib` – Core Utilities & Services

```text
src/lib/
├── db.ts                      # MongoDB connection setup
├── auth.ts                    # Auth helpers (tokens, hashing)
├── mdx.ts                     # MDX parsing (if used in Phase 1)
├── logger.ts                  # Logging helpers (optional)
├── validation/
│   ├── article-schema.ts      # Zod or similar validation
│   ├── user-schema.ts
│   └── comment-schema.ts
└── utils.ts                   # Generic helpers (slug, formatting)
```

---

## 6. `src/models` – Database Schemas

```text
src/models/
├── User.ts
├── Category.ts
├── Tag.ts
├── Article.ts
├── Comment.ts
└── AdSlot.ts
```

Each file:

* Defines the Mongoose schema
* Exports the corresponding model

These map directly to the entities defined in the data model section of the main SRS.

---

## 7. `src/hooks` – Reusable Hooks

```text
src/hooks/
├── useLanguage.ts             # English/Hinglish toggle state
├── useAuth.ts                 # Current user session
├── usePagination.ts
├── useSearch.ts
└── useAnalytics.ts            # View/event tracking (client-side)
```

---

## 8. `src/types` – TypeScript Types

```text
src/types/
├── article.ts
├── user.ts
├── category.ts
├── tag.ts
├── comment.ts
└── index.ts                   # Optional, re-exports
```

Types should:

* Reflect the database models
* Be reused in API handlers, components, and hooks

---

## 9. `src/config` – Configuration & Constants

```text
src/config/
├── site.ts                    # Site name (Popverse), description, links
├── seo.ts                     # Default SEO metadata
├── routes.ts                  # Named route constants
└── env.ts                     # Safe environment variable access
```

---

## 10. `src/styles` & Middleware

```text
src/styles/
└── globals.css                # Tailwind + global styles

src/middleware.ts              # Protect /admin routes, auth checks
```

---

## 11. `scripts` – One-Time & Maintenance

```text
scripts/
└── migrate-mdx-to-mongo.ts    # MDX → MongoDB migration (Phase 2)
```

---

## 12. Acceptance Criteria

* All public pages and admin pages map clearly to the `app/` directory.
* Reusable components are grouped logically in `components/`.
* Data access and business logic are separated into `lib/` and `models/`.
* Types, hooks, and configs have dedicated folders.
* New features (e.g., newsletter, bookmarks) can be added by extending existing folders, not by restructuring the project.
