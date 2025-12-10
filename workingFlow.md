# ⚙️ Part 2 – Working Flow (Frontend Setup & Base UI)

## 1️⃣ Overview

This section describes the **initial working flow** required to set up the Popverse frontend environment and design core reusable UI components. These steps do not require backend integration and establish the foundation for future development.

---

## 2️⃣ Objectives

* Configure the complete frontend development environment
* Establish a consistent global layout structure
* Design essential UI elements that appear on every page
* Prepare static pages for Phase 1 content

---

## 3️⃣ Development Environment Requirements

### Software Requirements

| Item             | Requirement                  |
| ---------------- | ---------------------------- |
| Operating System | Windows / macOS / Linux      |
| Node.js          | Latest LTS version installed |
| Code Editor      | Visual Studio Code           |

### Recommended VS Code Extensions

* ESLint
* Prettier
* Tailwind CSS IntelliSense
* TypeScript Language Features

---

## 4️⃣ Framework & Libraries Used

| Layer         | Technology           |
| ------------- | -------------------- |
| Framework     | Next.js (App Router) |
| Language      | TypeScript           |
| Styling       | Tailwind CSS         |
| UI Components | shadcn/ui            |

---

## 5️⃣ Project Initialization Summary

The following configurations are completed after project creation:

* Next.js installed with App Router
* TypeScript enabled by default
* Tailwind CSS configured
* shadcn/ui initialized with reusable UI components

Result: The Popverse project environment is **fully ready for frontend development**.

---

## 6️⃣ Base UI Design Scope

At this stage, elements are focused only on frontend static design. No backend or database connectivity is required.

The following UI elements must be created:

### Global Layout Structure

* Header (Navigation Bar)
* Main page content area
* Footer (Global website info and links)

This layout will be shared across all pages.

---

## 7️⃣ Navigation Bar (Header) Requirements

**Component Name:** `Navbar`

### Functional & Design Specifications

| Requirement                | Details                                                                 |
| -------------------------- | ----------------------------------------------------------------------- |
| Branding                   | Popverse logo or text title at top-left                                 |
| Menu Navigation            | Links to: Home, Movies, Webseries, Anime, Comics, Mangas, Novels, Games |
| Language Support (UI Only) | English / Hinglish toggle placeholder                                   |
| Authentication (Later)     | Login / Signup buttons (Phase 2 integration)                            |
| Mobile Design              | Hamburger menu that opens a drawer                                      |
| Behaviour                  | Sticky on scroll (optional)                                             |

---

## 8️⃣ Footer Requirements

**Component Name:** `Footer`

### Content Specification

| Section         | Elements                                          |
| --------------- | ------------------------------------------------- |
| About Snippet   | Short description of Popverse and its purpose     |
| Important Links | About, Contact, Privacy Policy*, Terms* (*Future) |
| Social Section  | Icons placeholders (YouTube / Instagram / X)      |
| Legal Notice    | “© Popverse — All Rights Reserved”                |

Future expandability: Newsletter subscription integration

---

## 9️⃣ Static Pages (UI-Only)

The following pages must be created using placeholder content only:

| Page                  | URL            | Description                                                     |
| --------------------- | -------------- | --------------------------------------------------------------- |
| Home Page             | `/`            | Hero section + category highlights + dummy content placeholders |
| About                 | `/about`       | Project mission, goals, and vision                              |
| Login                 | `/login`       | Basic form UI, no real authentication yet                       |
| Signup                | `/signup`      | Basic registration UI only                                      |
| Category Listing Page | `/movies` etc. | Displays dummy article cards for each category                  |

All pages must be:

* Fully responsive
* SEO-friendly structure
* Consistent with the branding identity of Popverse

---

## 1️⃣0️⃣ Acceptance Criteria

| Condition                      | Status   |
| ------------------------------ | -------- |
| Environment fully set up       | Required |
| Navbar & Footer completed      | Required |
| Static pages visually designed | Required |
| No backend functionality       | Expected |
| UI reusable and scalable       | Required |

---

### ✔️ Completion Result

After completing this workflow:

* The **Popverse UI foundation** will be ready
* Future article data and authentication can be integrated without UI redesign

---

⏭️ Next Working Flow:

* Component structure & file organization guidelines
* Content input strategy for Phase 1 (dummy data or MDX planning)
