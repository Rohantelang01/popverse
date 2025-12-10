# 📑 Part 3 – Site Structure, Features & Data Model (Popverse)

## 1. Purpose of this Document

This part defines the **ultimate structure** of the Popverse website, including:

* Main sections and pages of the site
* Features available on each page
* How content will be organised and related
* Core data entities and their fields

This acts as a **blueprint** before implementing frontend or backend logic.

---

## 2. High-Level Site Structure

### 2.1 Public-Facing Sections

1. **Home Page** (`/`)
2. **Category Pages** (`/movies`, `/webseries`, `/anime`, `/comics`, `/mangas`, `/novels`, `/games`)
3. **Article Pages** (`/[category]/[slug]`)
4. **Static Pages**

   * About (`/about`)
   * Contact (optional, future) (`/contact`)
5. **Auth Pages** (Phase 2)

   * Login (`/login`)
   * Signup (`/signup`)
6. **Utility / Discovery (Future)**

   * Search (`/search?q=...`)
   * Tags (`/tags/[slug]`)

### 2.2 Admin / Internal Sections (Phase 2+)

1. **Admin Dashboard** (`/admin/dashboard`)
2. **Article Management** (`/admin/articles`)
3. **Comments Moderation** (`/admin/comments`)
4. **Categories & Tags Management** (`/admin/categories`, `/admin/tags`)
5. **Ad Management** (`/admin/ads`)
6. **User Management** (`/admin/users`)
7. **Analytics** (`/admin/analytics`)

---

## 3. Page-Level Feature Definitions

### 3.1 Home Page (`/`)

**Goal:** Provide an overview of recent and important content across Popverse.

**Key Sections:**

* Hero area with featured article
* Latest articles list (across all categories)
* Category highlights (7 fixed categories)
* Trending or popular articles (by views/likes)
* Global language switch (English / Hinglish)

**Data Required:**

* List of published articles with basic info
* Category metadata

---

### 3.2 Category Page (`/[category]`)

**Goal:** Show all content for a specific category (e.g., Movies, Anime).

**Features:**

* Category title and description
* Paginated list of articles in that category
* Filters (later): by tags, date, type (News / Review / Recommendation)
* Sidebar with popular tags and/or top articles in that category

**Data Required:**

* Category object
* Article list filtered by category
* Tags used in this category (optional)

---

### 3.3 Article Page (`/[category]/[slug]`)

**Goal:** Display a single piece of content (news, review, or recommendation).

**Features:**

* Cover image
* Title (English + Hinglish)
* Article content (English + Hinglish)
* Language toggle
* Category & tags
* Author details
* Publish date and status
* View count and like count (Phase 2+)
* Social share buttons (WhatsApp, X, Facebook, etc.)
* Related articles section
* Comments section (Phase 2)
* Ad slots (header / inline / sidebar)

**Data Required:**

* Single Article object
* Linked Category object
* Linked Tags list
* Linked Author (User) object
* Comments list (Phase 2)

---

### 3.4 About Page (`/about`)

**Goal:** Explain what Popverse is, who it is for, and the mission.

**Content:**

* Description of the project
* Goals (learning + content platform)
* Future vision (community, features)

**Data Required:**

* Static content (no dynamic data required initially)

---

### 3.5 Login & Signup Pages (`/login`, `/signup`) – Phase 2

**Goal:** Allow users to create accounts and log in.

**Features (UI + Backend in Phase 2):**

* Login via email + password
* Signup with name, email, password
* Basic validation and error messages

**Data Required:**

* User records
* Authentication logic (backend)

---

### 3.6 Admin Pages (Phase 2+)

Each admin page focuses on managing a specific part of the system:

* Dashboard → statistics
* Articles → CRUD operations for content
* Comments → moderation
* Categories & Tags → taxonomy control
* Ads → manage ad slots
* Users → manage roles
* Analytics → traffic and performance data

---

## 4. Content Types (Data Entities)

This section defines **what data** the system will store and how entities relate to each other.

### 4.1 Entity List

* User
* Category
* Tag
* Article
* Comment
* AdSlot

---

### 4.2 User

Represents anyone who can log in (admin or standard user).

**Key Fields (Conceptual):**

* `id`
* `name`
* `email` (unique)
* `passwordHash`
* `role` (user / admin)
* `createdAt`
* `updatedAt`

**Used For:**

* Attribution (article author)
* Authentication
* Comment ownership

---

### 4.3 Category

Represents one of the **seven fixed content categories**.

**Categories (fixed set):**

* Movies
* Webseries
* Anime
* Comics
* Mangas
* Novels
* Games

**Key Fields:**

* `id`
* `name` (e.g., "Movies")
* `slug` (e.g., `movies`)
* `description`
* `createdAt`

**Used For:**

* Grouping articles
* Building category pages

---

### 4.4 Tag

Represents a label used to further describe articles (e.g., Action, Thriller, Marvel).

**Key Fields:**

* `id`
* `name`
* `slug`
* `usageCount` (number of articles using this tag)
* `createdAt`

**Used For:**

* Filtering and discovery
* Popular tags section

---

### 4.5 Article (Core Content Entity)

Represents news, reviews, or recommendation content.

**Key Field Groups:**

**Identity & URLs:**

* `id`
* `slug` (unique, used in URL)

**Language Variants:**

* `title_en`
* `summary_en`
* `content_en`
* `title_hi` (Hinglish)
* `summary_hi`
* `content_hi`

**Media:**

* `coverImageUrl`
* `coverImageAlt`

**Classification:**

* `categoryId` (link to Category)
* `tagIds[]` (list of Tag ids)
* `type` (news / review / recommendation – optional field)

**Author & Publishing:**

* `authorId` (link to User)
* `status` (draft / published / scheduled)
* `publishedAt`
* `scheduledFor` (optional)

**Engagement (Phase 2+):**

* `views`
* `likes`

**SEO:**

* `metaDescription_en`
* `metaDescription_hi`
* `metaKeywords[]`

**Review-Specific (optional):**

* `isReview`
* `rating` (1–5)
* `pros[]`
* `cons[]`

**System Fields:**

* `createdAt`
* `updatedAt`

---

### 4.6 Comment (Phase 2)

Represents user discussions on articles.

**Key Fields:**

* `id`
* `articleId` (link to Article)
* `userId` (link to User)
* `content`
* `parentId` (for replies / nested comments, can be null)
* `isFlagged`
* `isDeleted`
* `createdAt`
* `updatedAt`

**Usage:**

* Threaded comment structure
* Moderation

---

### 4.7 AdSlot (Phase 2+)

Represents a configurable advertisement area on the website.

**Key Fields:**

* `id`
* `name` (e.g., Header Banner)
* `position` (header / sidebar / inline / footer)
* `type` (html / image / script)
* `content` (for HTML / script)
* `imageUrl` (for image ads)
* `clickUrl`
* `isActive`
* `createdAt`
* `updatedAt`

**Usage:**

* Show or hide ads dynamically
* Place ads in article and category pages

---

## 5. Relationships Between Entities

### 5.1 Relationship Diagram (Conceptual)

* **User → Article**: One User can author many Articles
* **User → Comment**: One User can write many Comments
* **Category → Article**: One Category can have many Articles
* **Tag ↔ Article**: Many-to-many (each article can have multiple tags and each tag can belong to multiple articles)
* **Article → Comment**: One Article can have many Comments
* **Comment → Comment**: One Comment can have many replies (via `parentId`)

---

## 6. Language Handling Concept

* All main content is stored in **two manual language versions**:

  * English
  * Hinglish
* Language switch happens on the **frontend UI** without changing the URL.
* For each article, both language variants are part of the same Article entity.
* Future: automatic translation can be added as a separate process, but is **not part of the MVP**.

---

## 7. Phasing of Features

### Phase 1 (MVP)

* Home, Category, Article, About pages
* Manual content (e.g., MDX or seeded data)
* Basic multi-language support (content already written in both languages)
* No login, comments, or admin panel yet

### Phase 2

* Database integration (MongoDB)
* Admin panel for content creation
* Authentication (login/signup)
* Comments
* Basic ads and analytics

### Phase 3 (Optional Enhancements)

* Advanced search and filters
* Newsletter
* Advanced analytics
* Social / community features

---

## 8. Acceptance Criteria for Structure & Model

* All major pages and routes are defined
* Core entities and fields are clearly listed
* Relationships between entities are documented
* Language strategy is defined
* Phase-wise boundaries are clear (what is in MVP vs later)

This completes the **conceptual structure and data model** for Popverse and will guide all further frontend and backend implementation decisions.