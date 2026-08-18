# **FRONTEND EVOLUTION - COMPREHENSIVE PROJECT DOCUMENTATION**

## **EXECUTIVE SUMMARY**

**FrontendEvolution** is a Next.js-based SaaS platform designed for frontend engineer interview preparation. It provides structured study paths, 500+ interview questions (organized by topic, company, and difficulty), company-specific guides, and real-time progress tracking with certificate generation. The application is built for modern frontend development with a focus on performance, accessibility, and user experience.

**Core Value Proposition:**
- Structured learning paths (Junior → Mid → Senior levels)
- Company-specific interview guides (Google, Meta, Amazon, etc.)
- Progress persistence and achievement tracking
- Certificate generation on study completion
- Dark mode support with system preference detection

**Technology Stack:**
- **Frontend**: React 19.2.4, Next.js 16 App Router, Tailwind CSS 4
- **Backend**: Next.js API Routes (server components + serverless functions)
- **Database**: PostgreSQL with Prisma 6.16.1 ORM
- **Authentication**: NextAuth.js (credentials + GitHub/Google OAuth)
- **Deployment**: ISR (Incremental Static Regeneration) with GitHub webhook

---

## **PROJECT OVERVIEW**

### **What Problem Does This Solve?**

Frontend engineers preparing for interviews face fragmented resources:
- Interview questions scattered across multiple sources
- No unified tracking of preparation progress
- Company-specific evaluation patterns undocumented
- No structured learning path to optimize study time
- Lack of measurable achievement/certification

FrontendEvolution consolidates these into one platform with:
1. **Centralized Question Bank** - 500+ questions from external markdown repository
2. **Structured Study Plans** - Curated paths by difficulty (Junior/Mid/Senior)
3. **Company Intelligence** - Tailored guides per tech company's evaluation patterns
4. **Progress Persistence** - Track completed questions, bookmarks, time invested
5. **Achievement Recognition** - Generate certificates on plan completion

### **Primary Purpose**

An interview preparation SaaS platform that combines expert-curated content with personalized progress tracking, enabling engineers to optimize their preparation timeline and measure competency gains.

### **Target Users**

- Frontend engineers preparing for interviews (junior to senior level)
- Career changers transitioning into frontend roles
- Tech professionals brushing up on fundamental skills
- Students learning web development

### **Core Features**

| Feature | Purpose | Status |
|---------|---------|--------|
| User Authentication | Secure account creation and login | ✅ Implemented (Credentials + OAuth) |
| Study Plans | Structured learning paths by difficulty | ✅ Implemented (Junior/Mid/Senior) |
| Question Bank | 500+ interview questions searchable by topic | ✅ Implemented (external markdown) |
| Progress Tracking | Mark questions complete, sync across devices | ✅ Implemented (real-time sync) |
| Bookmarks | Save questions for later review | ✅ Implemented |
| Company Guides | Curated questions by company | ✅ Implemented |
| Certificates | PDF certificates on study plan completion | ✅ Implemented |
| Dark Mode | System preference + manual toggle | ✅ Implemented |
| Blog | Educational articles and insights | 🚧 Partially implemented (mock data) |
| Guides | In-depth tutorial sections | 🚧 Partially implemented (mock data) |

### **Main Workflows**

```
Guest User                          Authenticated User
    ↓                                      ↓
Browse Questions/Companies    →    Dashboard (progress overview)
    ↓                                      ↓
View Question Details         →    Mark Complete / Bookmark
    ↓                                      ↓
Prompted to Sign Up/Login     →    Activate Study Plan
    ↓                                      ↓
Create Account or OAuth       →    Track Progress
    ↓                                      ↓
Redirect & Execute Pending    →    Generate Certificate
Action (mark-complete/bookmark)           ↓
    ↓                                 Download PDF
View Personalized Dashboard   →    Share Certificate
```

---

## **REPOSITORY STRUCTURE ANALYSIS**

### **Root Configuration Files**

**`package.json`** - Project metadata and dependencies
- Manages 16 npm packages (React, Next, Prisma, NextAuth, etc.)
- Scripts: `dev`, `build`, `start`, `lint`, `validate:content`, `build:content-index`, `prisma:generate`, `prisma:migrate`

**`tsconfig.json`** - TypeScript configuration
- Target: ES2017, strict mode enabled
- Path alias: `@/*` → `./src/*`

**`next.config.ts`** - Next.js configuration
- Currently minimal (no custom config)

**`tailwind.config.ts`** - Tailwind CSS configuration
- Tailwind 4 with PostCSS support

**`postcss.config.mjs`** - PostCSS setup
- Tailwind plugin integration

**`eslint.config.mjs`** - ESLint configuration
- Next.js ESLint config

---

### **Folder: `app` - Application Routes & Pages**

**Purpose**: Contains Next.js 16 App Router pages and API routes. Follows file-based routing convention.

**Structure**:
```
src/app/
├── globals.css                 # Global Tailwind styles
├── layout.tsx                  # Root layout (auth session + theme init)
├── sitemap.ts                  # XML sitemap generation
├── (marketing)/                # Public routes group
│   ├── layout.tsx              # Marketing layout (header/footer)
│   └── page.tsx                # Home/landing page
├── (shell)/                    # Authenticated routes group
│   ├── layout.tsx              # Shell layout (page wrapper)
│   ├── blog/                   # Blog articles
│   ├── certificates/[id]/      # Certificate detail pages
│   ├── companies/              # Company guides listing
│   ├── companies/[slug]/       # Company-specific questions
│   ├── dashboard/              # User dashboard (protected)
│   ├── guides/                 # Learning guides
│   ├── guides/[guideSlug]/     # Guide detail
│   ├── guides/[guideSlug]/[articleSlug]/  # Guide article detail
│   ├── login/                  # Login page
│   ├── privacy/                # Privacy policy
│   ├── questions/              # Question listing with filters
│   ├── questions/[slug]/       # Question detail page
│   ├── settings/               # User settings
│   ├── signup/                 # Sign up page
│   ├── study-plans/            # Study plan listing
│   └── study-plans/[slug]/     # Study plan detail
└── api/                        # API routes
    ├── auth/[...nextauth]/     # NextAuth endpoint
    ├── auth/signup             # Email/password signup
    ├── me/
    │   ├── bookmarks           # Bookmark CRUD
    │   ├── preferences         # User settings API
    │   ├── progress            # Progress tracking
    │   ├── progress/[contentId] # Delete progress entry
    │   └── study-plans/[id]/   # Study plan operations
    │       ├── activate        # Activate study plan
    │       └── certificate     # Generate certificate PDF
    └── revalidate              # GitHub webhook for ISR
```

**Key Files by Category**:

**Root Layout** - `layout.tsx`
- Initializes session, theme preference, and providers
- Applies fonts (Inter, Geist Mono)
- Sets up HTML dark class based on theme
- Wraps with SessionProvider, ThemeProvider, PendingActionExecutor

**Authentication Pages**:
- src/app/(shell)/login/page.tsx/login/page.tsx) - Credentials + OAuth login
- src/app/(shell)/signup/page.tsx/signup/page.tsx) - Account creation
- [src/app/api/auth/[...nextauth]/route.ts](src/app/api/auth/[...nextauth]/route.ts) - NextAuth handler
- `route.ts` - Signup endpoint

**Protected Pages** (require authentication):
- src/app/(shell)/dashboard/page.tsx/dashboard/page.tsx) - Shows active study plan progress, recent completions, bookmarks
- src/app/(shell)/settings/page.tsx/settings/page.tsx) - User profile and preferences
- [src/app/(shell)/certificates/[id]/page.tsx](src/app/(shell)/certificates/[id]/page.tsx) - Certificate details

**Content Pages** (public):
- src/app/(shell)/questions/page.tsx/questions/page.tsx) - Question browser with filters
- src/app/(shell)/companies/page.tsx/companies/page.tsx) - Company listing
- src/app/(shell)/study-plans/page.tsx/study-plans/page.tsx) - Study plan listing
- src/app/(shell)/blog/page.tsx/blog/page.tsx) - Blog articles
- src/app/(shell)/guides/page.tsx/guides/page.tsx) - Learning guides

**API Routes**:
- `route.ts` - GET (sync progress), POST (mark complete)
- `route.ts` - GET, POST, DELETE bookmarks
- `route.ts` - PATCH user settings
- [src/app/api/me/study-plans/[id]/activate/route.ts](src/app/api/me/study-plans/[id]/activate/route.ts) - Activate study plan
- [src/app/api/me/study-plans/[id]/certificate/route.ts](src/app/api/me/study-plans/[id]/certificate/route.ts) - Generate PDF certificate
- `route.ts` - GitHub webhook for ISR

**Dependencies**: All pages use React Server Components except client-side forms/interactions marked with `"use client"`. Depends on Prisma for DB access, NextAuth for auth, and utility functions from `lib`.

**Usage Flow**: 
1. User navigates to route → Next.js App Router matches file-based path
2. If page is async component, data fetched server-side
3. Session/theme context provided by root layout
4. Client components hydrate for interactive features

---

### **Folder: `components` - React Components**

**Purpose**: Reusable UI components and layout wrappers.

**Components by Category**:

**Layout Components**:
- `page-shell.tsx` - Page wrapper with header/footer and centered max-width container
- `site-header.tsx` - Navigation header with logo, nav links, theme toggle, user menu
- `site-footer.tsx` - Footer with links and metadata

**Authentication Components**:
- `login-form.tsx` - Credentials login form + OAuth button links
- `signup-form.tsx` - Registration form with email/password, auto-login on signup
- `session-provider.tsx` - NextAuth SessionProvider wrapper

**Theme & Providers**:
- `theme-provider.tsx` - React Context for theme state (light/dark/system)
- `theme-toggle.tsx` - Theme switcher button

**Content & Dashboard**:
- `content-action-buttons.tsx` - Mark Complete / Bookmark buttons (handles auth redirect for guests)
- `content-action-buttons.tsx` - "Mark Complete" and "Bookmark" CTAs on question pages
- `markdown-content.tsx` - Renders markdown with syntax highlighting and responsive styling
- `dashboard-sync-beacon.tsx` - Syncs progress across browser tabs/windows
- `company-avatar.tsx` - Company logo/name badge

**User Settings**:
- `settings-form.tsx` - Name and theme preference form
- `study-plan-activate-button.tsx` - Activate study plan CTA

**Utilities**:
- `pending-action-executor.tsx` - Executes deferred actions (bookmark/mark-complete) after guest signup

**Component Hierarchy**:
```
App Root
├── SessionProvider
├── ThemeProvider
├── PendingActionExecutor
│
├── Marketing Routes
│   └── MarketingLayout
│       ├── SiteHeader
│       ├── Main Content
│       └── SiteFooter
│
└── Shell Routes
    └── PageShell
        ├── SiteHeader
        ├── PageContent
        │   ├── ContentActionButtons
        │   ├── MarkdownContent
        │   └── StudyPlanActivateButton
        └── SiteFooter
```

**Styling**: All components use Tailwind CSS with dark mode class toggle (`dark:` prefix). Colors and spacing defined as CSS variables in `globals.css`.

**Dependencies**: 
- `next-auth/react` - Session and sign out
- `next/navigation` - Router, pathname
- React hooks (useState, useContext, useEffect, useCallback)
- Internal utilities from `lib`

---

### **Folder: `lib` - Business Logic & Utilities**

**Purpose**: Core application logic, database access, content processing, and helper functions.

**Critical Files**:

**`auth.ts`** - Authentication Configuration
- Exports `authOptions` (NextAuth configuration) and `nextAuthHandler`
- Providers: Credentials (email/password), GitHub OAuth (optional), Google OAuth (optional)
- Credentials validation: email format + password ≥8 chars, bcryptjs password comparison
- Adapters: PrismaAdapter for DB persistence
- Session strategy: JWT (stateless)
- Callbacks:
  - `jwt`: Enriches token with user theme preference and subscription tier
  - `session`: Attaches user ID and preferences to session object
- Pages: Custom sign-in redirect to `/login`

**`prisma.ts`** - Database Client
- Singleton Prisma client instance
- Dev logging: errors and warnings
- Prod logging: errors only
- Prevents multiple instances in development

**`auth-helpers.ts`** - Auth Utilities
- `getAuthedUserId()` - Gets current user ID from session (server-side)
- `unauthorizedJson()` - Returns 401 JSON response

**`content-index.ts`** - Content Management (Server-Only)
- Reads pre-generated `content-index.json` from build step
- Fallback to mock data if file doesn't exist
- Exports cached functions:
  - `getContentIndex()` - Returns full index (questions, companies, cheatsheets)
  - `getContentQuestions()` - Array of all questions
  - `getQuestionBySlug(slug)` - Single question lookup
  - `getQuestionFacets()` - Aggregated filters (topics, formats, difficulties, companies)
  - `getCompanies()` - Unique companies with slugified names

**`mock-data.ts`** - Fallback Data
- Hardcoded questions, study plans, blog posts, guides for development/fallback
- Structures:
  - `Question`: slug, title, description, topic, format, difficulty, framework, companies
  - `StudyPlan`: slug, title, track (junior/mid/senior), items array
  - `BlogPost`: slug, title, description, publishedAt
  - `Guide`: slug, title, articles array

**`content-repo-validation.ts`** - Content Validation
- Fetches markdown from external GitHub repo: `frontendevolution/frontend-evolution-questions-and-cheatsheets`
- Validates frontmatter: topic, difficulty, format, framework (placeholders filtered)
- Checks for missing companies, empty bodies, duplicates
- Used by build script and webhook revalidation
- Exits with status 1 on violations

**`study-plans.ts`** - Study Plan Management
- `ensureStudyPlansSeeded()` - Syncs mock study plans to DB (upserts by slug)
- `getStudyPlanBySlug(slug)` - Retrieves study plan with items
- `resolveStudyPlanByIdOrSlug(input)` - Looks up by ID first, then slug

**`certificates.ts`** - Certificate Generation
- `createCertificatePdfBuffer()` - Generates PDF using pdf-lib
- Template: Blue border, learner name, study plan title, issue date, certificate ID
- Returns PDF bytes for data URL or file save

**`pending-action.ts`** - Guest Action Deferral
- Encodes/decodes pending actions to URL params
- Types: "mark-complete", "bookmark"
- Used for capturing guest intent before auth redirect
- `completePendingAction()` - Executes deferred action after login

**`theme.ts`** - Theme Utilities
- Type guard: `isThemePreference()`
- Cookie name: `fe_theme`
- Values: "light" | "dark" | "system"

**`seo.ts`** - SEO Metadata
- Site URL from env or fallback

**`revalidation.ts`** - ISR Revalidation Logic
- Parses GitHub webhook payload
- Extracts changed files from commits
- Maps file paths to routes:
  - `InterviewQuestions/` → `/questions/{slug}`
  - `TechBasedQuestions/` → `/questions/{slug}`
  - `cheatsheets/` → `/questions/{slug}`
  - `CompanyBasedQuestions/` → `/companies/{slug}`
- Always revalidates: `/questions`, `/companies`, `/sitemap.xml`
- Returns affected paths for revalidatePath()

**Dependencies**: 
- Prisma, NextAuth, bcryptjs, zod (validation), pdf-lib, gray-matter, react-markdown
- External: GitHub API for content validation

---

### **Folder: `hooks` - Custom React Hooks**

**`use-progress-sync.ts`** - Cross-Tab Progress Sync
- Polls `/api/me/progress?since={lastSync}` at regular intervals (default 45s)
- Fetches progress updates since last sync timestamp
- Triggers on tab focus, visibility change, and timer
- Called in DashboardSyncBeacon component to keep progress in sync
- Prevents duplicate syncs with `sinceRef`

---

### **Folder: `types` - TypeScript Definitions**

**`next-auth.d.ts`** - NextAuth Type Extensions
- Extends `Session.user` with: `id`, `themePreference`, `subscriptionTier`
- Extends `JWT` with: `themePreference`, `subscriptionTier`

---

### **Folder: `prisma` - Database Schema & Migrations**

**`schema.prisma`** - Database Schema

**Enums**:
```prisma
enum ContentType { article, question }
enum SubscriptionTier { free, premium }
enum ThemePreference { light, dark, system }
```

**Models**:

1. **User** - User account
   - Fields: id (cuid), name, email (unique), emailVerified, image, passwordHash, subscriptionTier, themePreference, activeStudyPlanId, createdAt, updatedAt
   - Relations: accounts, sessions, progress, bookmarks, certificates, activeStudyPlan

2. **Account** - OAuth account linking (NextAuth Prisma Adapter)
   - Composite ID: provider + providerAccountId
   - OAuth tokens stored here

3. **Session** - Session tokens (NextAuth)
   - sessionToken (unique), userId, expires

4. **VerificationToken** - Email verification (NextAuth)
   - Composite ID: identifier + token

5. **StudyPlan** - Learning path structure
   - Fields: id (cuid), slug (unique), title, description, createdAt, updatedAt
   - Relations: items (StudyPlanItem), activeUsers (User)

6. **StudyPlanItem** - Individual plan item
   - Fields: id, studyPlanId, title, order (for sequencing), contentType, contentId
   - Composite index: (studyPlanId, order)

7. **Progress** - Question completion tracking
   - Fields: id, userId, contentType, contentId, completedAt, updatedAt
   - Composite unique: (userId, contentType, contentId)
   - Ordered by updatedAt for sync

8. **Bookmark** - Saved questions
   - Fields: id, userId, contentType, contentId, createdAt
   - Composite unique: (userId, contentType, contentId)

9. **Certificate** - Study plan completion certificate
   - Fields: id, userId, studyPlanId, issuedAt, pdfUrl (data URL), verificationUrl
   - Indexed by (userId, issuedAt)

**`migration.sql`** - Initial Schema
- Creates all enums and tables
- Establishes foreign key relationships with onDelete CASCADE

---

### **Folder: `scripts` - Build & Validation Scripts**

**`build-content-index.mjs`** - Content Index Generator
- Validates external markdown repo
- If validation passes, generates `content-index.json`
- Exits with code 1 on validation errors
- Called via: `npm run build:content-index`

**`validate-content-repo.mjs`** - Validation Only
- Performs same validation without generating index
- Called via: `npm run validate:content`

**`content-repo-utils.mjs`** - Shared Utilities
- Common functions for validation scripts
- Configurable BRANCH via env or default "main"

---

### **Folder: `public` - Static Assets**
Empty in current structure. Can contain images, favicons, robots.txt, etc.

---

### **Folder: `generated` - Build Artifacts**

**`content-index.json`** - Generated at Build Time
- Metadata: generatedAt, source (owner, repo, branch)
- Array of questions with: id, slug, path, title, description, publishedAt, topic, format, difficulty, framework, companies, body
- Lookup maps: companyQuestionMap (company → question slugs), cheatsheetLinks (slug → cheatsheet URL)
- Created by `build-content-index.mjs` before Next.js build

---

## **APPLICATION STARTUP FLOW**

### **Step-by-Step Execution Sequence**

```mermaid
flowchart TD
    A["npm run dev / npm run build"] --> B["Next.js Build Process Starts"]
    B --> C["Execute Build Scripts"]
    C --> D["validate-content-repo.mjs"]
    D --> E{Validation<br/>Passes?}
    E -->|No| F["Exit Code 1<br/>Build Fails"]
    E -->|Yes| G["build-content-index.mjs"]
    G --> H["Generate src/generated/content-index.json"]
    H --> I["Next.js Builds App"]
    I --> J["Compile TypeScript"]
    J --> K["Bundle Assets"]
    K --> L["npm start or Dev Server"]
    L --> M["Browser Request"]
    M --> N["Root Layout Executes<br/>src/app/layout.tsx"]
    N --> O["Call auth<br/>Get session"]
    O --> P["Read cookies<br/>Load theme"]
    P --> Q["Initialize Providers"]
    Q --> R["AppSessionProvider<br/>NextAuth SessionProvider"]
    Q --> S["ThemeProvider<br/>with resolved theme"]
    Q --> T["PendingActionExecutor<br/>Watches for guest actions"]
    Q --> U["Child Page Renders"]
    U --> V["Page-specific Data Fetch<br/>Prisma queries"]
    V --> W["Server Component<br/>Renders HTML"]
    W --> X["Client-side Hydration<br/>React 19 interactivity"]
    X --> Y["Page Interactive"]
```

### **Detailed Startup Steps**

**1. Build Time (Pre-Runtime)**
- Content validation runs (`validate-content-repo.mjs`)
  - Fetches markdown from GitHub repo
  - Validates frontmatter structure
  - Checks for duplicates, overlaps, missing companies
- Content index generation (`build-content-index.mjs`)
  - Creates `content-index.json` if validation passes
- Next.js compilation
  - TypeScript → JavaScript
  - CSS module bundling
  - Server component optimization

**2. Runtime - Server Start**
- Next.js server starts (dev mode: `next dev`, prod: `next start`)
- Prisma client initializes singleton
- Environment variables loaded

**3. Request Handling - First Page Load**
1. Browser requests root path (`/`)
2. Next.js routes to src/app/(marketing)/page.tsx/page.tsx) or src/app/(shell)/*/*) depending on path
3. Root layout (`layout.tsx`) executes:
   - Calls `auth()` → Gets NextAuth session
   - Reads cookies → Gets theme preference
   - Initializes theme value (cookie → session → system preference fallback)
   - Renders `<html>` with dark class if needed

**4. Provider Initialization**
- AppSessionProvider wraps with NextAuth SessionProvider
  - Enables `useSession()` client hook
  - Manages auth state
- ThemeProvider wraps with theme context
  - Tracks theme state (light/dark/system)
  - Listens to system preference changes
  - Exposes `useTheme()` hook
- PendingActionExecutor mounts
  - Watches search params for pending actions
  - Executes deferred bookmarks/completions after auth
  - Cleans up params from URL

**5. Page Component Renders**
- Page component (server component) executes
- Makes authenticated data fetches via Prisma
- Renders static HTML + hydration markers
- Client components receive initial props

**6. Client Hydration**
- React 19 hydrates interactive components
- Event listeners attached
- State initialized from props
- Page becomes fully interactive

---

## **SYSTEM ARCHITECTURE**

### **Architecture Style: Hybrid Modular + Layered**

**Why This Architecture?**

The application combines:
1. **Modular by Feature** - Related components (auth, questions, study-plans) grouped logically
2. **Layered by Concern** - Separation between pages, components, business logic, persistence
3. **Next.js App Router Routing** - File-based routing with built-in server/client split
4. **Database-Driven** - Prisma ORM abstracts persistence layer

This hybrid approach provides:
- **Scalability** - Easy to add new features (e.g., new question type)
- **Maintainability** - Clear separation of concerns
- **Flexibility** - Mix of server and client rendering per need
- **Performance** - ISR + static optimization where possible

---

### **High-Level Architecture Diagram**

```mermaid
graph TB
    subgraph "Client Layer"
        Browser["Browser / Client App"]
        Components["React Components<br/>Login, Dashboard, Questions"]
        Hooks["Custom Hooks<br/>useProgressSync, useTheme"]
    end
    
    subgraph "API Layer"
        APIAuth["API Routes<br/>auth/signup<br/>auth/[...nextauth]"]
        APIMeProgress["API Routes<br/>me/progress<br/>me/bookmarks<br/>me/preferences"]
        APIStudyPlan["API Routes<br/>study-plans/activate<br/>study-plans/certificate"]
        APIRevalidate["API Routes<br/>revalidate<br/>GitHub Webhook"]
    end
    
    subgraph "Business Logic Layer"
        AuthLogic["Authentication<br/>NextAuth Config<br/>bcryptjs"]
        ContentLogic["Content Management<br/>Index Generation<br/>Validation"]
        StudyPlanLogic["Study Plan Logic<br/>Seeding<br/>Lookup"]
        CertLogic["Certificate Generation<br/>PDF Creation"]
    end
    
    subgraph "Data Access Layer"
        Prisma["Prisma ORM<br/>Query Builder"]
        Validation["Content Repo Validation<br/>GitHub API"]
    end
    
    subgraph "Database Layer"
        PostgreSQL["PostgreSQL Database<br/>User, Progress, Bookmarks<br/>StudyPlan, Certificate"]
    end
    
    subgraph "External Services"
        GitHub["GitHub<br/>OAuth Provider<br/>Content Repo<br/>Webhooks"]
        Google["Google<br/>OAuth Provider"]
    end
    
    Browser -->|HTTP Requests| APIAuth
    Browser -->|HTTP Requests| APIMeProgress
    Browser -->|HTTP Requests| APIStudyPlan
    Components --> Hooks
    
    APIAuth --> AuthLogic
    APIMeProgress --> StudyPlanLogic
    APIStudyPlan --> CertLogic
    APIRevalidate --> Validation
    
    AuthLogic --> Prisma
    StudyPlanLogic --> Prisma
    CertLogic --> Prisma
    ContentLogic --> Validation
    
    Prisma --> PostgreSQL
    Validation --> GitHub
    AuthLogic --> GitHub
    AuthLogic --> Google
```

---

### **Layer Responsibilities**

**Client Layer (Frontend)**
- React Server Components: Handle data fetching server-side, render HTML
- Client Components: Interactive UI (forms, buttons, theme toggle)
- Hooks: Encapsulate stateful logic (auth session, theme, progress sync)

**API Layer (Server Routes)**
- Validate requests (auth, input schema)
- Call business logic
- Return JSON responses or file streams
- Handle errors (400, 401, 404, 409)

**Business Logic Layer**
- Authentication (NextAuth, credentials validation, OAuth)
- Content processing (validation, index generation)
- Study plan management (seeding, lookup, activation)
- Certificate generation (PDF rendering)

**Data Access Layer (Prisma)**
- Query building and execution
- Relationship loading
- Type-safe database operations
- Transaction support

**Database Layer**
- Persistent storage for all entities
- Constraints and validation at DB level
- Indexes for performance

**External Services**
- GitHub: OAuth provider, content source, webhooks
- Google: OAuth provider

---

### **Module Relationships**

```mermaid
graph LR
    subgraph "Pages/Routes"
        Marketing["(marketing)<br/>Landing Page"]
        Dashboard["(shell)/dashboard<br/>Progress View"]
        Questions["(shell)/questions<br/>Browse & Filter"]
        Companies["(shell)/companies<br/>Company Guides"]
        StudyPlans["(shell)/study-plans<br/>Plan Listing"]
        Auth["(shell)/login/signup<br/>Auth Pages"]
    end
    
    subgraph "Components"
        Forms["LoginForm<br/>SignupForm<br/>SettingsForm"]
        Actions["ContentActionButtons<br/>StudyPlanActivateButton"]
        Display["MarkdownContent<br/>CompanyAvatar"]
        Layout["PageShell<br/>SiteHeader<br/>SiteFooter"]
    end
    
    subgraph "Hooks & Providers"
        Session["AppSessionProvider<br/>useSession"]
        Theme["ThemeProvider<br/>useTheme"]
        Sync["useProgressSync<br/>Dashboard Beacon"]
    end
    
    subgraph "API Handlers"
        SignupAPI["POST /api/auth/signup"]
        ProgressAPI["GET/POST /api/me/progress"]
        BookmarkAPI["GET/POST/DELETE /api/me/bookmarks"]
        PrefAPI["PATCH /api/me/preferences"]
        StudyPlanAPI["POST /api/me/study-plans/[id]/activate"]
        CertAPI["POST /api/me/study-plans/[id]/certificate"]
    end
    
    subgraph "Business Logic"
        AuthLib["src/auth.ts<br/>NextAuth Config"]
        StudyLib["study-plans.ts<br/>Seeding & Lookup"]
        CertLib["certificates.ts<br/>PDF Generation"]
        ContentLib["content-index.ts<br/>Question Loading"]
        ValidLib["content-repo-validation.ts<br/>Validation"]
    end
    
    subgraph "Database"
        Prisma["Prisma Client"]
        DB["PostgreSQL"]
    end
    
    Dashboard --> Session
    Dashboard --> Sync
    Dashboard --> Theme
    Questions --> Actions
    StudyPlans --> Actions
    Auth --> Forms
    Forms --> Session
    Actions --> ProgressAPI
    Actions --> BookmarkAPI
    Dashboard --> ContentLib
    SignupAPI --> AuthLib
    ProgressAPI --> StudyLib
    CertAPI --> CertLib
    StudyPlanAPI --> StudyLib
    AuthLib --> Prisma
    StudyLib --> Prisma
    CertLib --> Prisma
    ContentLib --> ValidLib
    Prisma --> DB
```

---

### **Dependency Flow**

```
Deepest (No Dependencies)
    ↓
PostgreSQL Database (external system)
    ↓
Prisma ORM (queries database)
    ↓
Business Logic Layer (auth.ts, study-plans.ts, certificates.ts)
    ↓
API Routes (use business logic)
    ↓
Components (call API routes)
    ↓
Pages (compose components)
    ↓
Root Layout & Providers (initialize app)
    ↓
Browser (renders final output)
```

**No Circular Dependencies**: Architecture is strictly layered - components don't import from pages, API routes don't import from components.

---

## **ROUTING ANALYSIS**

### **Route Map**

| Route | Page Component | Purpose | Auth Required | Type | Middleware |
|-------|----------------|---------|---|------|----------|
| `/` | src/app/(marketing)/page.tsx/page.tsx) | Landing/home page | No | Public | None |
| `/login` | src/app/(shell)/login/page.tsx/login/page.tsx) | Email + OAuth login | No | Public | Redirect if already authed |
| `/signup` | src/app/(shell)/signup/page.tsx/signup/page.tsx) | Account creation | No | Public | Redirect if already authed |
| `/dashboard` | src/app/(shell)/dashboard/page.tsx/dashboard/page.tsx) | User dashboard | **Yes** | Protected | Redirect to /login if not authed |
| `/settings` | src/app/(shell)/settings/page.tsx/settings/page.tsx) | User preferences | **Yes** | Protected | Redirect to /login |
| `/questions` | src/app/(shell)/questions/page.tsx/questions/page.tsx) | Browse questions with filters | No | Public | None |
| `/questions/[slug]` | [src/app/(shell)/questions/[slug]/page.tsx](src/app/(shell)/questions/[slug]/page.tsx) | Question detail | No | Public | None |
| `/companies` | src/app/(shell)/companies/page.tsx/companies/page.tsx) | Company listing | No | Public | None |
| `/companies/[slug]` | [src/app/(shell)/companies/[slug]/page.tsx](src/app/(shell)/companies/[slug]/page.tsx) | Company-specific questions | No | Public | None |
| `/study-plans` | src/app/(shell)/study-plans/page.tsx/study-plans/page.tsx) | Study plan listing | No | Public | None |
| `/study-plans/[slug]` | [src/app/(shell)/study-plans/[slug]/page.tsx](src/app/(shell)/study-plans/[slug]/page.tsx) | Study plan detail + activate | No | Public | None (activation requires auth) |
| `/certificates/[id]` | [src/app/(shell)/certificates/[id]/page.tsx](src/app/(shell)/certificates/[id]/page.tsx) | Certificate detail + download | No | Public | None |
| `/guides` | src/app/(shell)/guides/page.tsx/guides/page.tsx) | Learning guides listing | No | Public | None |
| `/guides/[guideSlug]` | [src/app/(shell)/guides/[guideSlug]/page.tsx](src/app/(shell)/guides/[guideSlug]/page.tsx) | Guide detail | No | Public | None |
| `/guides/[guideSlug]/[articleSlug]` | [src/app/(shell)/guides/[guideSlug]/[articleSlug]/page.tsx](src/app/(shell)/guides/[guideSlug]/[articleSlug]/page.tsx) | Guide article | No | Public | None |
| `/blog` | src/app/(shell)/blog/page.tsx/blog/page.tsx) | Blog articles | No | Public | None |
| `/privacy` | src/app/(shell)/privacy/page.tsx/privacy/page.tsx) | Privacy policy | No | Public | None |
| `/terms` | src/app/(shell)/terms/page.tsx/terms/page.tsx) | Terms of service | No | Public | None |
| `/sitemap.xml` | `sitemap.ts` | XML sitemap | No | Public | None |

**API Routes**:

| Endpoint | Method | Purpose | Auth Required | Request | Response |
|----------|--------|---------|---|---------|----------|
| `/api/auth/[...nextauth]` | GET, POST | NextAuth handler | No | Varies | NextAuth responses |
| `/api/auth/signup` | POST | Email/password signup | No | `{ name, email, password }` | 201: `{ user }` or 400/409 |
| `/api/me/progress` | GET | Fetch progress updates | **Yes** | Query: `?since=ISO8601` | 200: `{ items: Progress[] }` |
| `/api/me/progress` | POST | Mark question complete | **Yes** | `{ content_type, content_id }` | 201: `{ progress }` |
| `/api/me/progress/[contentId]` | DELETE | Delete progress entry | **Yes** | Body: `{ content_type, content_id }` | 200 or 404 |
| `/api/me/bookmarks` | GET | Fetch bookmarks | **Yes** | None | 200: `{ items: Bookmark[] }` |
| `/api/me/bookmarks` | POST | Add bookmark | **Yes** | `{ content_type, content_id }` | 201: `{ bookmark }` |
| `/api/me/bookmarks` | DELETE | Remove bookmark | **Yes** | `{ content_type, content_id }` | 200 or 404 |
| `/api/me/preferences` | PATCH | Update user settings | **Yes** | `{ name, theme }` | 200: `{ user }` |
| `/api/me/study-plans/[id]/activate` | POST | Activate study plan | **Yes** | None | 200: `{ plan }` or 404/400 |
| `/api/me/study-plans/[id]/certificate` | POST | Generate certificate | **Yes** | None | 201: `{ certificate }` or 400/404 |
| `/api/revalidate` | POST | GitHub webhook for ISR | Optional (secret auth) | GitHub push payload | 200: `{ revalidated: boolean }` |

**Route Organization**:

```
Marketing Routes (Public, Landing Focus)
  └── (marketing)
      ├── / (landing page)
      └── layout.tsx (header + footer)

Shell Routes (Authenticated + Public Content)
  └── (shell)
      ├── layout.tsx (page shell with header + footer)
      ├── /dashboard (protected)
      ├── /login, /signup (auth)
      ├── /settings (protected)
      ├── /questions (public)
      ├── /companies (public)
      ├── /study-plans (public)
      ├── /guides (public)
      ├── /blog (public)
      ├── /certificates (public)
      └── /privacy, /terms (public)

API Routes
  └── api/
      ├── auth/ (NextAuth + signup)
      ├── me/ (protected user data)
      └── revalidate (GitHub webhook)
```

**Route Groups** (`(marketing)` and `(shell)`) allow different layouts without affecting URL:
- Different header/footer styling
- Different max-width constraints
- Different background colors

**Dynamic Routes** use `[slug]` or `[id]` syntax:
- `/questions/[slug]` - Matches `/questions/react-hooks`, `/questions/css-flexbox`, etc.
- `/companies/[slug]` - Matches `/companies/google`, `/companies/meta`, etc.
- Slug derived from markdown filename or database record

---

### **Static vs. Dynamic Routes**

**Statically Generated (Build Time, Revalidated via ISR)**:
- `/` - Landing page
- `/login`, `/signup` - Auth forms
- `/questions` - Question listing with facets
- `/companies` - Company directory
- `/study-plans` - Study plan directory
- `/blog`, `/guides` - Content pages

**Dynamically Rendered (On-Demand)**:
- `/dashboard` - Protected, user-specific data
- `/settings` - Protected, user-specific
- `/api/me/*` - Personalized API responses
- `/certificates/[id]` - Certificate detail

**ISR Revalidation Triggers** (Incremental Static Regeneration):
- GitHub webhook on push to main branch
- Validates content repository
- Revalidates affected paths (question detail pages, company pages, sitemap)
- Runs `revalidatePath()` for efficiency

---

### **Middleware & Route Guards**

**Implicit Guards** (at page level):
- src/app/(shell)/dashboard/page.tsx/dashboard/page.tsx) - Calls `redirect()` if no session
- src/app/(shell)/settings/page.tsx/settings/page.tsx) - Calls `redirect()` if not authed

**API Guards**:
- All `/api/me/*` routes call `getAuthedUserId()` and return 401 if missing
- Example: `route.ts`

**Pending Action Handling** (`pending-action-executor.tsx`):
- Watches for `?pendingAction=<encoded>` URL param
- Executes after guest signup/login
- Auto-removes param from URL afterward

---

## **UI COMPONENT ARCHITECTURE**

### **Component Tree Overview**

```
App
├── (RootLayout)
│   ├── <html> + dark mode class
│   ├── AppSessionProvider (NextAuth)
│   ├── ThemeProvider (React Context)
│   ├── PendingActionExecutor (Effect hook)
│   │
│   ├── (marketing)
│   │   └── MarketingLayout
│   │       ├── SiteHeader (logo, nav, theme toggle)
│   │       ├── Main: <children>
│   │       └── SiteFooter
│   │
│   └── (shell)
│       └── ShellLayout
│           └── PageShell
│               ├── SiteHeader
│               ├── Main Container (max-w-[1440px], padding)
│               │   ├── Dashboard
│               │   │   ├── DashboardSyncBeacon (useProgressSync hook)
│               │   │   ├── Welcome Header
│               │   │   ├── Progress Bar
│               │   │   ├── Study Plan Preview
│               │   │   ├── Recent Completions
│               │   │   └── Bookmarks List
│               │   │
│               │   ├── Questions Page
│               │   │   ├── Filter Sidebar (faceted search)
│               │   │   └── Question Cards Grid
│               │   │       ├── Question Card
│               │   │       ├── ContentActionButtons
│               │   │       │   ├── Mark Complete Button
│               │   │       │   └── Bookmark Button
│               │   │       └── Difficulty Badge
│               │   │
│               │   ├── Question Detail
│               │   │   ├── Question Header
│               │   │   ├── MarkdownContent (rendered markdown)
│               │   │   ├── ContentActionButtons
│               │   │   ├── Metadata (topic, difficulty, company)
│               │   │   └── Related Questions
│               │   │
│               │   ├── Study Plans
│               │   │   └── StudyPlanCard[]
│               │   │       ├── Difficulty Badge
│               │   │       ├── Title & Description
│               │   │       ├── StudyPlanActivateButton
│               │   │       └── Item Count & Estimated Hours
│               │   │
│               │   ├── Study Plan Detail
│               │   │   ├── Plan Header
│               │   │   ├── Progress Bar
│               │   │   ├── StudyPlanActivateButton / Certificate Button
│               │   │   └── Plan Items List
│               │   │       └── Item Card
│               │   │           ├── Checkbox (if authenticated)
│               │   │           └── Title + Link
│               │   │
│               │   ├── Companies
│               │   │   └── CompanyCard[]
│               │   │       ├── CompanyAvatar
│               │   │       ├── Company Name
│               │   │       ├── Question Count
│               │   │       └── View Guide Link
│               │   │
│               │   └── Settings
│               │       ├── Profile Section
│               │       └── SettingsForm
│               │           ├── Name Input
│               │           ├── Theme Select (system/light/dark)
│               │           └── Save Button
│               │
│               └── SiteFooter
```

### **Component Reusability & Props**

**High-Reusability Components** (Used Multiple Places):

1. **ContentActionButtons**
   ```typescript
   type Props = {
     contentType: "article" | "question";
     contentId: string;
   };
   // Used on: question cards, question detail, study plan items
   ```
   - Handles auth logic (redirect guests to signup with pending action)
   - Shows loading states
   - Posts to `/api/me/progress` or `/api/me/bookmarks`

2. **CompanyAvatar**
   ```typescript
   type Props = {
     name: string;
     slug: string;
     size?: "sm" | "md" | "lg";
   };
   // Used on: company listing, question metadata
   ```

3. **MarkdownContent**
   ```typescript
   type Props = {
     source: string;
   };
   // Used on: question detail, guide articles, certificate pages
   ```
   - Renders markdown with syntax highlighting
   - Responsive typography and spacing

**Medium-Reusability Components**:

4. **PageShell** - Wraps shell-layout pages with header/footer
5. **SiteHeader** - Top navigation (used by both marketing and shell layouts)
6. **SiteFooter** - Footer (used by both layouts)

**Low-Reusability (Page-Specific)**:

7. **LoginForm** - Only on `/login`
8. **SignupForm** - Only on `/signup`
9. **SettingsForm** - Only on `/settings`
10. **DashboardSyncBeacon** - Only on `/dashboard`

---

### **Client vs. Server Components**

**Server Components** (Default, async allowed):
- Page components: `dashboard/page.tsx`, `questions/page.tsx`, `questions/[slug]/page.tsx`
- Reasons: Data fetching at request time, access to DB, auth check, SEO

**Client Components** (marked `"use client"`):
- `login-form.tsx` - Form submission, error state
- `signup-form.tsx` - Form submission
- `settings-form.tsx` - Form submission
- `content-action-buttons.tsx` - User action handlers
- `theme-provider.tsx` - React Context
- `session-provider.tsx` - NextAuth provider
- `pending-action-executor.tsx` - useEffect hook
- `site-header.tsx` - Interactive menu + theme toggle
- `theme-toggle.tsx` - Theme switcher
- `study-plan-activate-button.tsx` - Action handler

**Why This Split?**
- Server components reduce JS bundle size
- Client components enable interactivity without full page hydration
- Prevents unnecessary state management on server

---

## **STATE MANAGEMENT ANALYSIS**

### **State Architecture**

This application uses a **distributed state model** rather than centralized Redux/Zustand:

```mermaid
graph TB
    subgraph "Server-Side State"
        DBState["Database State<br/>Prisma Queries<br/>- User profile<br/>- Progress records<br/>- Bookmarks<br/>- Study plans"]
        SessionState["Session State<br/>NextAuth JWT<br/>- User ID<br/>- Email<br/>- Theme pref<br/>- Subscription tier"]
    end
    
    subgraph "Client-Side State"
        ReactState["React Component State<br/>useState hooks<br/>- Form inputs<br/>- Loading flags<br/>- Error messages"]
        ContextState["React Context<br/>- Session context<br/>- Theme context<br/>- Pending actions"]
        BrowserState["Browser Storage<br/>- Cookies (theme)<br/>- SessionStorage"]
    end
    
    subgraph "Sync Mechanism"
        APISync["API Requests<br/>- POST /api/me/progress<br/>- POST /api/me/bookmarks<br/>- PATCH /api/me/preferences"]
        ProgressSync["useProgressSync Hook<br/>Polls every 45s<br/>Updates on focus/visible"]
    end
    
    DBState -->|Query| SessionState
    SessionState -->|Sent to Client| ContextState
    ReactState -->|User Actions| APISync
    APISync -->|Updates| DBState
    ProgressSync -->|Sync Latest| DBState
```

### **State Storage Locations**

**1. Database (Persistent, Server Source of Truth)**
```typescript
// User data
User { id, email, name, themePreference, activeStudyPlanId, ... }

// User actions
Progress { userId, contentId, completedAt, ... }
Bookmark { userId, contentId, createdAt, ... }
Certificate { userId, studyPlanId, pdfUrl, ... }

// Content structure
StudyPlan { slug, title, items[] }
```

**2. Session (JWT, Ephemeral)**
```typescript
// NextAuth Session stored in:
// - JWT cookie (encrypted, httpOnly)
// - In-memory on client (useSession hook)

Session {
  user: {
    id: string;
    email: string;
    name: string;
    themePreference: "light" | "dark" | "system";
    subscriptionTier: "free" | "premium";
  }
}
```

**3. React Context (Client, Ephemeral)**
```typescript
// Theme Context
ThemeContext {
  theme: "light" | "dark" | "system";
  resolvedTheme: "light" | "dark";
  setTheme: (nextTheme) => void;
}

// Session Context (from NextAuth)
// Accessed via useSession() hook
```

**4. Component State (Local, Ephemeral)**
```typescript
// Form inputs
const [email, setEmail] = useState("");
const [password, setPassword] = useState("");
const [loading, setLoading] = useState(false);
const [error, setError] = useState(null);
```

**5. Browser Storage (Persistent Client)**
```javascript
// Theme cookie (fallback if DB not synced yet)
Cookie: fe_theme=dark; Path=/; Max-Age=2592000

// Session token (managed by NextAuth)
Cookie: next-auth.session-token=...
```

### **Data Synchronization Strategy**

**Question 1: How Does Progress Get Synced Across Tabs?**

Answer: useProgressSync Hook
```typescript
// Polls /api/me/progress?since={lastSyncTime} every 45s
// Also triggers on:
//   - Tab visibility change (visible)
//   - Window focus
//   - Page navigation

// Updates tracked via updatedAt timestamp
// Prevents redundant syncs
```

**Question 2: How Does Theme Persist?**

Answer: Cookie + Context
```
1. Server-side: Read theme from DB or cookie
2. Pass to client via props
3. Client: ThemeProvider reads initial theme
4. On change: Save cookie + update context
5. Cookie survives until session ends
6. On login: DB preference used
```

**Question 3: How Does Auth Persist?**

Answer: NextAuth JWT Cookie
```
1. User logs in → NextAuth creates JWT
2. JWT stored in httpOnly cookie (secure)
3. Cookie sent with every request
4. On each request: JWT decoded, session validated
5. Session enriched with DB data (theme, subscription)
6. Logout: Cookie cleared
```

### **Cache Strategy**

**Build-Time Caching**:
```typescript
// Content index generated once at build
// Revalidated only on GitHub webhook or manual rebuild
// Fallback to mock data if missing
```

**Request-Time Caching** (React `cache()`):
```typescript
// getContentIndex() wrapped with React.cache()
// Prevents duplicate DB queries in same request
// Scoped to single page render

export const getContentIndex = cache(async () => {
  // Runs once per request, even if called multiple times
  return loadIndex();
});
```

**Client-Side Caching**:
```typescript
// useProgressSync: Tracks `since` timestamp
// Only fetches updates newer than last sync
// Prevents re-fetching old data
```

---

## **AUTHENTICATION & AUTHORIZATION**

### **Authentication Flow Diagram**

```mermaid
sequenceDiagram
    participant User
    participant Browser
    participant NextAuth
    participant API
    participant Prisma
    participant Database
    
    User->>Browser: Visit /login
    Browser->>API: GET /login page
    API-->>Browser: LoginForm component
    
    User->>Browser: Enter email + password
    Browser->>Browser: Form submit event
    Browser->>NextAuth: signIn('credentials', {email, password})
    
    NextAuth->>API: Validate credentials
    API->>Database: findUser WHERE email=?
    Database-->>API: User record + passwordHash
    
    API->>API: bcryptjs.compare(password, hash)
    alt Password matches
        API-->>NextAuth: { id, email, name, image }
        NextAuth->>Database: Create/update Session
        NextAuth->>Browser: Set JWT cookie
        Browser-->>User: Redirect to /dashboard
    else Password invalid
        API-->>NextAuth: null
        NextAuth-->>Browser: Error message
        Browser-->>User: Show error
    end
```

### **Registration Flow**

```mermaid
sequenceDiagram
    participant User
    participant Browser
    participant SignupAPI
    participant Prisma
    participant Database
    participant Credentials
    
    User->>Browser: Visit /signup
    Browser->>Browser: SignupForm render
    
    User->>Browser: Enter name, email, password
    Browser->>SignupAPI: POST /api/auth/signup
    
    SignupAPI->>SignupAPI: Parse & validate JSON
    SignupAPI->>SignupAPI: Zod schema validation
    
    alt Invalid input
        SignupAPI-->>Browser: 400 Invalid payload
        Browser-->>User: Show error
    end
    
    SignupAPI->>Database: findUser WHERE email=?
    alt Email exists
        Database-->>SignupAPI: User found
        SignupAPI-->>Browser: 409 Email in use
        Browser-->>User: Show error
    end
    
    SignupAPI->>SignupAPI: hash(password, 12) with bcryptjs
    SignupAPI->>Database: CREATE User
    Database-->>SignupAPI: New user record
    
    SignupAPI-->>Browser: 201 { user }
    Browser->>Credentials: signIn('credentials', {email, password})
    Credentials->>Database: Verify credentials
    Credentials-->>Browser: JWT cookie set
    Browser-->>User: Redirect to /dashboard
```

### **OAuth Flow (GitHub Example)**

```mermaid
sequenceDiagram
    participant User
    participant Browser
    participant App
    participant GitHub
    participant Database
    
    User->>Browser: Click "Sign in with GitHub"
    Browser->>App: GET /api/auth/signin/github
    App->>GitHub: Redirect + client_id + redirect_uri
    
    GitHub-->>User: Authorize app?
    User->>GitHub: Click authorize
    
    GitHub->>App: Redirect with auth code
    App->>GitHub: POST token endpoint (code, secret)
    GitHub-->>App: { access_token, user_data }
    
    App->>Database: findUser WHERE email=github_email
    alt User exists
        Database-->>App: User found
    else New user
        App->>Database: CREATE User (from GitHub profile)
    end
    
    App->>Database: CREATE/UPDATE Account (OAuth link)
    App->>Browser: Set JWT + session cookie
    Browser-->>User: Redirect to /dashboard
```

### **Session Management**

**Session Strategy: JWT**

- Stateless: JWT contains all user data
- Stored in httpOnly cookie (secure)
- Can't be accessed from JavaScript (CSRF protection)
- Sent with every request automatically

**JWT Payload** (managed by NextAuth):
```typescript
{
  sub: "user_id",           // Subject (user ID)
  email: "user@email.com",
  name: "User Name",
  image: "avatar_url",
  themePreference: "dark",  // Added by callback
  subscriptionTier: "free", // Added by callback
  iat: 1234567890,          // Issued at
  exp: 1234571490,          // Expires
  iss: "nextauth.js",       // Issuer
}
```

**Session Enrichment** (in jwt callback):
```typescript
async jwt({ token, user }) {
  if (user?.id) {
    token.sub = user.id;
  }
  
  // Load user preferences from DB on each request
  if (token.sub) {
    const dbUser = await prisma.user.findUnique({
      where: { id: token.sub },
      select: { themePreference: true, subscriptionTier: true },
    });
    token.themePreference = dbUser?.themePreference ?? "system";
    token.subscriptionTier = dbUser?.subscriptionTier ?? "free";
  }
  
  return token;
}
```

### **Authorization Model**

**Current Model: Simple Authentication-Based**

- **Unauthenticated**: Can view questions, companies, study plans, blog, guides
- **Authenticated**: Can additionally:
  - Mark questions complete
  - Bookmark questions
  - View personal dashboard
  - Change settings
  - Activate study plans
  - Generate certificates

**Future Model (Not Yet Implemented)**:
- Premium vs. Free tier (SubscriptionTier enum exists but not enforced)
- Role-based (admin for content management)
- Permission checks on API endpoints

### **Security Considerations**

**Strong Points**:
1. ✅ Passwords hashed with bcryptjs (salt rounds: 12)
2. ✅ JWT in httpOnly cookie (not XSS-accessible)
3. ✅ Credentials validation with Zod schema
4. ✅ Email uniqueness constraint at DB level
5. ✅ API endpoints check session before mutation

**Potential Issues** (see Security Audit section below):
1. ⚠️ No CSRF protection on state-changing requests (should add SameSite cookie)
2. ⚠️ No rate limiting on signup endpoint (vulnerable to brute force)
3. ⚠️ No email verification (anyone can register any email)
4. ⚠️ Webhook secret is optional (GitHub webhook can be replayed)
5. ⚠️ No input sanitization on content-action-buttons (though Zod validates)

---

## **DATABASE ANALYSIS**

### **Database Type & Setup**

**PostgreSQL** with **Prisma 6.16.1 ORM**

**Connection**: Specified via `DATABASE_URL` env var
```bash
postgresql://user:password@host:port/database
```

### **Entity-Relationship Diagram**

```mermaid
erDiagram
    USER ||--o{ ACCOUNT : has
    USER ||--o{ SESSION : has
    USER ||--o{ PROGRESS : creates
    USER ||--o{ BOOKMARK : creates
    USER ||--o{ CERTIFICATE : owns
    USER ||--o| STUDYPLAN : "active"
    STUDYPLAN ||--o{ STUDYPLANITEM : contains
    STUDYPLAN ||--o{ CERTIFICATE : "issued_for"
    
    USER {
        string id PK
        string name
        string email UK
        datetime emailVerified
        string image
        string passwordHash
        enum subscriptionTier
        enum themePreference
        string activeStudyPlanId FK
        datetime createdAt
        datetime updatedAt
    }
    
    ACCOUNT {
        string userId FK
        string type
        string provider
        string providerAccountId
        string refresh_token
        string access_token
        int expires_at
        string token_type
        string scope
        string id_token
        string session_state
    }
    
    SESSION {
        string sessionToken UK
        string userId FK
        datetime expires
    }
    
    VERIFICATIONTOKEN {
        string identifier
        string token UK
        datetime expires
    }
    
    STUDYPLAN {
        string id PK
        string slug UK
        string title
        string description
        datetime createdAt
        datetime updatedAt
    }
    
    STUDYPLANITEM {
        string id PK
        string studyPlanId FK
        string title
        int order
        enum contentType
        string contentId
    }
    
    PROGRESS {
        string id PK
        string userId FK
        enum contentType
        string contentId
        datetime completedAt
        datetime updatedAt
    }
    
    BOOKMARK {
        string id PK
        string userId FK
        enum contentType
        string contentId
        datetime createdAt
    }
    
    CERTIFICATE {
        string id PK
        string userId FK
        string studyPlanId FK
        datetime issuedAt
        string pdfUrl
        string verificationUrl
    }
```

### **Schema Details**

**Enums**:
```prisma
enum ContentType { article, question }
enum SubscriptionTier { free, premium }
enum ThemePreference { light, dark, system }
```

**User Model**:
- Stores both local (password) and OAuth accounts
- activeStudyPlanId: Nullable foreign key to active study plan
- subscriptionTier: Currently unused (future feature)
- themePreference: Synced with client-side cookie

**Account Model** (NextAuth Adapter):
- Links OAuth providers to users
- Stores OAuth tokens for future API calls
- Composite PK: (provider, providerAccountId)

**Session Model** (NextAuth Adapter):
- Used only if session strategy is "database" (currently using JWT)
- Can be cleaned up for JWT-only approach

**Progress Model**:
- Tracks completion per content item
- Composite unique: (userId, contentType, contentId)
- Indexed by userId + updatedAt for efficient sync queries
- updatedAt triggers for cache invalidation

**Bookmark Model**:
- Same structure as Progress
- Composite unique prevents duplicate bookmarks
- Indexed for quick user bookmark retrieval

**StudyPlan & StudyPlanItem**:
- Plan: slug-based lookup for URL routing
- Items: ordered (important for sequence), contentId references external content
- No CASCADE delete on items (manual cleanup required)

**Certificate**:
- Links user + plan
- Stores generated PDF as data URL
- verificationUrl for public certificate verification
- Indexed by userId + issuedAt for user's certificate history

### **Data Flow: Read Operations**

**Question Detail Page Load**:
```
User visits /questions/react-hooks
  ↓
getQuestionBySlug("react-hooks")
  ↓
Load src/generated/content-index.json
  ↓
Find question in index array
  ↓
Render question with markdown body
  ↓
Check auth: if logged in, show ContentActionButtons
```

**Dashboard Load** (if authenticated):
```
User visits /dashboard
  ↓
auth() → get session
  ↓
prisma.user.findUnique({ where: { id: session.user.id } })
  ↓
Load activeStudyPlan with items
  ↓
prisma.progress.findMany({ where: { userId } })
  ↓
prisma.bookmark.findMany({ where: { userId } })
  ↓
Calculate progress % = completed / total
  ↓
Render dashboard
```

### **Data Flow: Write Operations**

**Mark Question Complete**:
```
User clicks "Mark Complete" button
  ↓
ContentActionButtons calls POST /api/me/progress
  ↓
getAuthedUserId() from session
  ↓
Validate payload: { content_type, content_id }
  ↓
prisma.progress.upsert({
  where: { userId_contentType_contentId },
  update: { completedAt: new Date() },
  create: { userId, contentType, contentId }
})
  ↓
Return updated progress
  ↓
Client state updates (optional)
  ↓
Next sync will fetch latest data
```

**Create Certificate**:
```
User completes study plan and clicks "Get Certificate"
  ↓
POST /api/me/study-plans/{id}/certificate
  ↓
getAuthedUserId()
  ↓
Fetch user, study plan, all progress
  ↓
Verify plan is active for user
  ↓
Check all plan items completed
  ↓
createCertificatePdfBuffer() → PDF bytes
  ↓
Generate UUID for certificate ID
  ↓
Create data URL from PDF
  ↓
prisma.certificate.create({
  id, userId, studyPlanId, issuedAt, pdfUrl, verificationUrl
})
  ↓
Return certificate
  ↓
Client downloads PDF from data URL
```

### **Database Constraints & Indexes**

**Unique Constraints**:
- User.email (unique)
- Account: (provider, providerAccountId)
- Session.sessionToken
- StudyPlan.slug
- Progress: (userId, contentType, contentId)
- Bookmark: (userId, contentType, contentId)

**Foreign Keys**:
- Account.userId → User.id (CASCADE DELETE)
- Session.userId → User.id (CASCADE DELETE)
- Progress.userId → User.id (CASCADE DELETE)
- Bookmark.userId → User.id (CASCADE DELETE)
- Certificate.userId → User.id (CASCADE DELETE)
- Certificate.studyPlanId → StudyPlan.id (CASCADE DELETE)
- User.activeStudyPlanId → StudyPlan.id (NO ACTION)
- StudyPlanItem.studyPlanId → StudyPlan.id (CASCADE DELETE)

**Indexes**:
- Progress: (userId, updatedAt) - For sync queries
- Bookmark: (userId, createdAt) - For listing
- Certificate: (userId, issuedAt) - For user certificate history
- StudyPlanItem: (studyPlanId, order) - For ordered retrieval

---

## **API DOCUMENTATION**

### **Authentication Endpoints**

**POST `/api/auth/signup`**
- **Purpose**: Create new account with email/password
- **Auth Required**: No
- **Request**:
  ```json
  {
    "name": "John Doe",
    "email": "john@example.com",
    "password": "securePassword123"
  }
  ```
- **Response (201)**:
  ```json
  {
    "user": {
      "id": "cuid123",
      "email": "john@example.com",
      "name": "John Doe"
    }
  }
  ```
- **Errors**:
  - 400: Invalid JSON or validation failure
  - 409: Email already in use

**GET/POST `/api/auth/[...nextauth]`**
- **Purpose**: NextAuth handler (login, OAuth, session)
- **Auth Required**: Varies
- **Supports**:
  - POST: Credentials login, OAuth callback
  - GET: Session retrieval, signin/signout pages

---

### **User Data Endpoints** (All require authentication)

**GET `/api/me/progress`**
- **Purpose**: Fetch user's progress records since timestamp
- **Query Params**:
  - `since` (optional): ISO 8601 timestamp
- **Response (200)**:
  ```json
  {
    "items": [
      {
        "contentType": "question",
        "contentId": "react-hooks:advanced",
        "completedAt": "2026-08-18T10:30:00Z",
        "updatedAt": "2026-08-18T10:30:00Z"
      }
    ]
  }
  ```

**POST `/api/me/progress`**
- **Purpose**: Mark content as complete
- **Request**:
  ```json
  {
    "content_type": "question",
    "content_id": "react-hooks:advanced"
  }
  ```
- **Response (201)**: Updated progress object

**DELETE `/api/me/progress/[contentId]`**
- **Purpose**: Remove completion marker
- **Response (200)**: Success or 404

**GET `/api/me/bookmarks`**
- **Purpose**: Fetch user's bookmarks
- **Response (200)**:
  ```json
  {
    "items": [
      {
        "contentType": "question",
        "contentId": "...",
        "createdAt": "..."
      }
    ]
  }
  ```

**POST `/api/me/bookmarks`**
- **Purpose**: Add or update bookmark (idempotent)
- **Request**:
  ```json
  {
    "content_type": "question",
    "content_id": "react-hooks"
  }
  ```
- **Response (201)**: Bookmark object

**DELETE `/api/me/bookmarks`**
- **Purpose**: Remove bookmark
- **Request**: Same as POST
- **Response (200)**: Success or 404

**PATCH `/api/me/preferences`**
- **Purpose**: Update user settings
- **Request**:
  ```json
  {
    "name": "Jane Doe",
    "theme": "dark"
  }
  ```
- **Response (200)**: Updated user object

**POST `/api/me/study-plans/[id]/activate`**
- **Purpose**: Set active study plan
- **Request**: Empty body
- **Response (200)**: Updated user with activeStudyPlan

**POST `/api/me/study-plans/[id]/certificate`**
- **Purpose**: Generate certificate PDF for completed study plan
- **Validation**: User must have completed all items in plan
- **Response (201)**:
  ```json
  {
    "id": "cert-uuid",
    "pdfUrl": "data:application/pdf;base64,...",
    "verificationUrl": "https://domain.com/certificates/cert-uuid"
  }
  ```
- **Errors**:
  - 400: Plan not completed
  - 404: Plan or user not found

---

### **Webhook Endpoint**

**POST `/api/revalidate`**
- **Purpose**: GitHub webhook for content updates
- **Headers**:
  - `x-hub-signature-256`: HMAC signature (validates via `GITHUB_WEBHOOK_SECRET`)
  - `x-revalidate-secret`: Alternative auth method
- **Query Params**:
  - `secret` (optional): Alternative to header
- **Request**: GitHub push payload
  ```json
  {
    "ref": "refs/heads/main",
    "commits": [
      {
        "added": [],
        "modified": ["InterviewQuestions/react-hooks.md"],
        "removed": []
      }
    ]
  }
  ```
- **Response (200)**:
  ```json
  {
    "revalidated": true,
    "paths": ["/questions", "/questions/react-hooks", "/sitemap.xml"]
  }
  ```
- **Errors**:
  - 401: Invalid signature or secret
  - 409: Content validation failed

---

### **Request/Response Patterns**

**All Authenticated Endpoints**:
- Check session: `await auth()`
- Return 401 if no session
- Validate payload with Zod
- Return 400 if invalid

**All Mutations** (POST, PATCH, DELETE):
- Accept JSON request body
- Use Zod for runtime validation
- Return 201 (created) or 200 (updated)
- Return error status on failure

**All Data Endpoints**:
- Use Prisma queries
- Select only necessary fields
- Use proper indexes for performance
- Cache results in React when appropriate

---

## **EXTERNAL INTEGRATIONS**

### **1. GitHub Integration**

**OAuth Provider**:
- Login with GitHub: `AUTH_GITHUB_ID`, `AUTH_GITHUB_SECRET`
- Configured in `auth.ts`
- User data: email, avatar, name

**Content Repository**:
- Repo: `frontendevolution/frontend-evolution-questions-and-cheatsheets`
- Branch: `main` (configurable via `CONTENT_REPO_BRANCH` env)
- Content: Markdown files in `InterviewQuestions/`, `TechBasedQuestions/`, `CompanyBasedQuestions/`, `cheatsheets/`

**GitHub API Usage** (in `content-repo-validation.ts`):
- `GET /repos/{owner}/{repo}/git/trees/{branch}?recursive=1` - List all files
- `GET /repos/{owner}/{repo}/contents/{path}` - Read file content

**Webhook Integration** (on POST /api/revalidate):
- GitHub sends push events to webhook URL
- Validates signature with `GITHUB_WEBHOOK_SECRET`
- Parses changed files
- Triggers ISR revalidation

---

### **2. Google OAuth**

**Provider**:
- Optional login: `AUTH_GOOGLE_ID`, `AUTH_GOOGLE_SECRET`
- Configured in `auth.ts`
- User data: email, name, picture

**Fallback**: If env vars not set, Google provider is disabled

---

### **3. NextAuth.js**

**Purpose**: Authentication framework
- Handles OAuth flows
- Manages JWT/session cookies
- Provides `useSession()` hook
- Integrates with Prisma

**Key Config**:
- Strategy: JWT (stateless)
- Custom pages: `/login`
- Adapters: PrismaAdapter for DB persistence

---

### **4. PDF Generation (pdf-lib)**

**Usage** (`certificates.ts`):
- Creates certificate PDF on study plan completion
- Embeds fonts, draws rectangles, text
- Returns PDF bytes
- Encoded as data URL for instant download

**Template**:
- Title: "Certificate of Completion"
- Content: Learner name, study plan title, issue date, certificate ID
- Styling: Blue border, professional layout

---

### **5. Markdown Processing**

**gray-matter**: Parses YAML frontmatter from markdown files
- Used in content validation to extract metadata
- Fields: title, topic, difficulty, format, framework, companies

**react-markdown**: Client-side markdown rendering
- Converts markdown body to HTML
- Plugins: remark-gfm (GitHub flavored markdown)
- Custom styling via Tailwind classes

---

## **BUILD & DEPLOYMENT PROCESS**

### **Build Steps**

```bash
# Local development
npm install
npm run prisma:generate    # Generate Prisma client
npm run dev                # Starts Next.js dev server

# Production build
npm run build              # Compiles and optimizes
npm start                  # Starts production server
```

**Build Script Execution** (before Next.js compile):

1. **Validate Content** (`validate-content-repo.mjs`)
   - Fetches markdown from GitHub repo
   - Validates frontmatter structure
   - Checks for violations (empty companies, placeholders, duplicates)
   - Exits with code 1 if invalid

2. **Generate Content Index** (`build-content-index.mjs`)
   - Runs validation (fails if invalid)
   - Processes all markdown files
   - Extracts metadata (title, topic, difficulty, etc.)
   - Creates lookup maps (companies → questions)
   - Writes `content-index.json`

3. **Next.js Build**
   - Compiles TypeScript
   - Bundles CSS/JS
   - Generates .next directory
   - Pre-renders static pages (ISR)

### **Deployment Architecture**

```mermaid
graph TB
    subgraph "Local Development"
        Dev["npm run dev"]
        Dev -->|Port 3000| Browser["Browser"]
    end
    
    subgraph "Build Phase"
        Scripts["Validation<br/>& Index Gen"]
        TypeScript["TypeScript<br/>Compilation"]
        Bundle["Asset<br/>Bundling"]
    end
    
    subgraph "Hosting"
        Server["Next.js Server<br/>Port 3000"]
        Cache["Static Files<br/>Cache"]
        DB["PostgreSQL<br/>Connection"]
    end
    
    subgraph "External"
        GitHub["GitHub<br/>OAuth<br/>Webhooks<br/>Content Repo"]
        Google["Google<br/>OAuth"]
    end
    
    Scripts -->|on success| TypeScript
    TypeScript --> Bundle
    Bundle -->|npm start| Server
    
    Browser -->|HTTP| Server
    Server -->|Prisma| DB
    Server -->|OAuth| GitHub
    Server -->|OAuth| Google
    GitHub -->|Webhook| Server
    Server -->|Serve| Cache
```

### **Environment Configuration**

**Required (Dev & Prod)**:
```bash
DATABASE_URL=postgresql://user:pass@host/db
NEXTAUTH_URL=https://domain.com      # For OAuth redirects
NEXTAUTH_SECRET=<random-64-char>     # JWT signing key
```

**Optional (OAuth)**:
```bash
AUTH_GITHUB_ID=<github-app-id>
AUTH_GITHUB_SECRET=<github-app-secret>
AUTH_GOOGLE_ID=<google-client-id>
AUTH_GOOGLE_SECRET=<google-client-secret>
```

**Optional (Webhooks & Content)**:
```bash
GITHUB_WEBHOOK_SECRET=<shared-secret>
REVALIDATE_SECRET=<shared-secret>
CONTENT_REPO_BRANCH=main              # Default: main
CONTENT_REPO_OWNER=frontendevolution  # In code (hardcoded)
```

**Development Only**:
```bash
NODE_ENV=development
NEXT_PUBLIC_SITE_URL=http://localhost:3000
```

### **Database Migrations**

```bash
# Create new migration
npm run prisma:migrate -- --name <name>

# Generate Prisma client after schema changes
npm run prisma:generate

# View database
npx prisma studio
```

**Current Migration** (`20260805065312_init`):
- Creates all enums
- Creates all tables with constraints
- Establishes relationships

### **Incremental Static Regeneration (ISR)**

**How It Works**:
1. Questions, companies, study plans pages are statically generated at build time
2. When GitHub webhook triggered:
   - Validates content
   - Determines changed files
   - Calls `revalidatePath()` for affected routes
   - Next.js regenerates only those pages in background
   - Old page served while regeneration happens
   - New page available immediately after

**Benefits**:
- Fast static serving (CDN-cacheable)
- Always up-to-date without full rebuild
- No downtime during updates

---

## **SECURITY AUDIT**

### **Critical Issues**

**1. MISSING RATE LIMITING** 🔴 HIGH RISK
- **Location**: `/api/auth/signup`
- **Issue**: No rate limit on signup endpoint
- **Impact**: Brute force attacks, email enumeration
- **Fix**: Implement rate limiting (e.g., Upstash Redis, `next-rate-limit`)
  ```typescript
  const rateLimit = new Ratelimit({
    redis: Redis.fromEnv(),
    limiter: Ratelimit.slidingWindow(5, "1 h"),
  });
  ```

**2. NO EMAIL VERIFICATION** 🔴 HIGH RISK
- **Location**: `/api/auth/signup`
- **Issue**: Users can register with fake emails
- **Impact**: Spam accounts, privacy abuse
- **Fix**: Add email verification flow
  ```typescript
  // Send verification email with token
  // Require verification before login
  ```

**3. MISSING CSRF PROTECTION ON STATE CHANGES** 🟡 MEDIUM RISK
- **Location**: All state-changing API routes
- **Issue**: CSRF tokens not validated
- **Impact**: Cross-site request forgery possible
- **Fix**: Ensure SameSite cookie attribute set to "Strict" (NextAuth default is "Lax")
  ```typescript
  // In middleware or NextAuth config
  cookies: {
    sessionToken: {
      options: {
        sameSite: "Strict"
      }
    }
  }
  ```

**4. OPTIONAL WEBHOOK SIGNATURES** 🟡 MEDIUM RISK
- **Location**: `/api/revalidate`
- **Issue**: `GITHUB_WEBHOOK_SECRET` is optional
- **Impact**: Webhook can be replayed by attackers
- **Fix**: Make webhook secret required or use GitHub's signature validation always
  ```typescript
  // Enforce validation
  if (!isValidGitHubSignature(...)) {
    return 401;  // Don't allow unsigned webhooks
  }
  ```

---

### **Medium Priority Issues**

**5. NO INPUT SANITIZATION** 🟡 MEDIUM RISK
- **Location**: MarkdownContent component, markdown files
- **Issue**: Raw markdown rendered without XSS protection
- **Impact**: Potential XSS if markdown contains script tags
- **Fix**: Use `react-markdown` safely (currently okay with `rehype-sanitize` plugin)
  ```typescript
  <ReactMarkdown
    remarkPlugins={[remarkGfm]}
    rehypePlugins={[rehypeSanitize]}  // Add this
  >
    {source}
  </ReactMarkdown>
  ```

**6. PASSWORD REQUIREMENTS TOO WEAK** 🟡 MEDIUM RISK
- **Location**: `/api/auth/signup`
- **Issue**: Only checks minimum 8 characters
- **Impact**: Weak passwords possible
- **Fix**: Add complexity requirements
  ```typescript
  const passwordSchema = z.string()
    .min(8)
    .regex(/[A-Z]/, "Must contain uppercase")
    .regex(/[0-9]/, "Must contain number")
    .regex(/[!@#$%]/, "Must contain special char");
  ```

**7. JWT EXPIRATION COULD BE LONGER** 🟡 MEDIUM RISK
- **Location**: NextAuth JWT config
- **Issue**: Default NextAuth JWT expiration might be long (check config)
- **Impact**: Stolen JWT could be used longer
- **Fix**: Set explicit short expiration
  ```typescript
  callbacks: {
    jwt({ token }) {
      token.exp = Math.floor(Date.now() / 1000) + (24 * 60 * 60); // 24 hours
      return token;
    }
  }
  ```

---

### **Low Priority Issues**

**8. NO AUDIT LOGGING** 🟢 LOW RISK
- **Location**: All API endpoints
- **Issue**: No logs of user actions
- **Impact**: Can't trace suspicious activity
- **Fix**: Add audit logging
  ```typescript
  await db.auditLog.create({
    userId, action: "mark_complete", contentId, timestamp: new Date()
  });
  ```

**9. SECRETS IN CODE** 🟢 LOW RISK (Mitigated)
- **Location**: Environment variables only
- **Status**: ✅ Good - All secrets in .env.local, not in code
- **Fix**: Document `.env.example` for required vars

**10. CERTIFICATE PDF DATA URLS** 🟢 LOW RISK
- **Location**: `/api/me/study-plans/*/certificate`
- **Issue**: PDF stored as data URL (large strings)
- **Impact**: Database bloat, slower queries
- **Fix**: Store PDFs externally (S3, R2) with URL reference
  ```typescript
  const pdfUrl = `https://cdn.example.com/certificates/${certificateId}.pdf`;
  // Instead of: data:application/pdf;base64,...
  ```

---

### **Security Checklist**

| Item | Status | Notes |
|------|--------|-------|
| Passwords hashed | ✅ | bcryptjs with 12 rounds |
| JWT in httpOnly cookie | ✅ | Secure, not JS-accessible |
| CORS properly configured | ✅ | Same-origin requests |
| SQL injection prevention | ✅ | Prisma parameterized queries |
| XSS prevention | ⚠️ | Needs sanitization on markdown |
| CSRF protection | ⚠️ | SameSite cookie helps but no explicit tokens |
| Rate limiting | ❌ | Missing on signup |
| Email verification | ❌ | Not implemented |
| Webhook signature validation | ⚠️ | Optional (should be required) |
| Audit logging | ❌ | Not implemented |
| Input validation | ✅ | Zod schemas on all APIs |

---

## **PERFORMANCE ANALYSIS**

### **Bundle Size Concerns**

**Large Dependencies**:
- `react-markdown` (~60KB) + `remark-gfm` - For markdown rendering
- `pdf-lib` (~150KB) - For certificate generation
- `next-auth` (~50KB) - For authentication

**Optimization Opportunities**:
1. **Dynamic imports** for markdown content (lazy load)
   ```typescript
   const MarkdownContent = dynamic(() => import('@/components/markdown-content'));
   ```

2. **PDF generation on server only** - Currently good (certificate route is server-side)

3. **Code splitting for OAuth** - Only load Google/GitHub SDKs if configured

### **Render Performance Issues**

**1. Dashboard Progress Calculation** 🟡 MEDIUM
- **Location**: src/app/(shell)/dashboard/page.tsx/dashboard/page.tsx)
- **Issue**: Calculates completion % on every page load
- **Fix**: Cache in database
  ```typescript
  model UserProgress {
    userId String
    totalCompleted Int
    lastUpdated DateTime
  }
  ```

**2. Content Index Full Load** 🟡 MEDIUM
- **Location**: `content-index.ts`
- **Issue**: Loads entire content-index.json into memory
- **Problem**: If 500+ questions, entire file parsed on each request
- **Fix**: Use pagination or streaming
  ```typescript
  // Implement pagination
  getContentQuestions(limit: 20, offset: 0)
  ```

**3. Study Plan Seeding on Each Request** 🟡 MEDIUM
- **Location**: `study-plans.ts`
- **Issue**: `ensureStudyPlansSeeded()` called on every study plan page load
- **Problem**: Doesn't re-query, but could be cached better
- **Fix**: Use database-level cache or one-time initialization
  ```typescript
  // Mark seeded in database
  model AppMetadata {
    key String @id
    value String
  }
  ```

### **Query Performance Issues**

**1. N+1 Problem** 🟡 MEDIUM
- **Location**: Dashboard when loading user + study plan + items
- **Issue**: Separate queries for user, plan, items
- **Fix**: Already using `include` (good), but verify all queries use eager loading

**2. Unindexed Progress Queries** ✅ GOOD
- **Status**: Composite index on (userId, updatedAt) exists
- **Impact**: Fast progress sync for `?since=` queries

**3. Missing Pagination** 🔴 HIGH
- **Location**: `/questions` page lists ALL questions
- **Issue**: If 500+ questions, loads all into memory
- **Fix**: Implement cursor-based pagination
  ```typescript
  const questions = await getContentQuestions();
  const paginated = questions.slice(cursor, cursor + PAGE_SIZE);
  ```

### **Optimization Wins (Already Implemented)**

✅ React Server Components - Reduced JS bundle
✅ Static Generation + ISR - Fast question page loads
✅ Proper database indexes - Fast lookups
✅ React.cache() - Prevents duplicate requests in single render
✅ useProgressSync batching - Efficient sync mechanism

### **Recommended Optimizations**

| Issue | Priority | Effort | Impact |
|-------|----------|--------|--------|
| Implement pagination for questions | HIGH | MEDIUM | Faster initial load |
| Add database caching for progress % | HIGH | SMALL | Faster dashboard |
| Lazy load markdown renderer | MEDIUM | SMALL | Smaller bundle |
| Move PDFs to external storage | MEDIUM | LARGE | Smaller database |
| Implement search indexing | MEDIUM | LARGE | Better UX |
| Add image optimization | LOW | MEDIUM | Faster load |
| Cache static content headers | LOW | SMALL | CDN caching |

---

## **DEVELOPER WORKFLOW**

### **How to Run Locally**

```bash
# 1. Clone and install
git clone <repo>
cd frontend-evolution
npm install

# 2. Setup environment
cp .env.example .env.local
# Edit .env.local with:
#   DATABASE_URL=postgresql://...
#   NEXTAUTH_URL=http://localhost:3000
#   NEXTAUTH_SECRET=<generate: openssl rand -base64 32>

# 3. Setup database
npm run prisma:generate
npm run prisma:migrate -- --name init

# 4. Start dev server
npm run dev

# 5. Visit http://localhost:3000
```

**Database Troubleshooting**:
```bash
# View database UI
npx prisma studio

# Reset database (DESTRUCTIVE)
npx prisma migrate reset

# Check migration status
npx prisma migrate status
```

---

### **How to Add a New Page**

**Example: Adding `/challenges` page**

1. **Create page file**:
   ```typescript
   // src/app/(shell)/challenges/page.tsx
   import Link from "next/link";
   
   export default async function ChallengesPage() {
     return (
       <div>
         <h1>Challenges</h1>
         <p>Coming soon...</p>
       </div>
     );
   }
   ```

2. **Add route to nav** `site-header.tsx`:
   ```typescript
   const navItemsGuest = [
     { href: "/challenges", label: "Challenges" },
     // ...
   ];
   ```

3. **Optional: Add to database schema** if needs data:
   ```prisma
   model Challenge {
     id String @id @default(cuid())
     slug String @unique
     title String
     description String
   }
   ```

4. **Generate Prisma client**:
   ```bash
   npm run prisma:generate
   npm run prisma:migrate -- --name add_challenges
   ```

5. **Test locally**:
   ```bash
   npm run dev
   # Visit http://localhost:3000/challenges
   ```

---

### **How to Add a New API Route**

**Example: Adding `/api/challenges` GET endpoint**

1. **Create route file**:
   ```typescript
   // src/app/api/challenges/route.ts
   import { NextResponse } from "next/server";
   import { prisma } from "@/lib/prisma";
   
   export async function GET(request: Request) {
     const challenges = await prisma.challenge.findMany({
       orderBy: { createdAt: "desc" },
       select: { id: true, title: true, slug: true }
     });
     
     return NextResponse.json({ challenges });
   }
   ```

2. **Add validation** if mutating:
   ```typescript
   import { z } from "zod";
   
   const createSchema = z.object({
     title: z.string().min(1),
     description: z.string().min(10),
   });
   
   export async function POST(request: Request) {
     const payload = await request.json();
     const parsed = createSchema.safeParse(payload);
     
     if (!parsed.success) {
       return NextResponse.json({ error: "Invalid" }, { status: 400 });
     }
     
     // ... handle
   }
   ```

3. **Add authentication if needed**:
   ```typescript
   import { getAuthedUserId, unauthorizedJson } from "@/lib/auth-helpers";
   
   export async function POST(request: Request) {
     const userId = await getAuthedUserId();
     if (!userId) return unauthorizedJson();
     
     // ... handle
   }
   ```

4. **Call from client**:
   ```typescript
   const response = await fetch("/api/challenges", {
     method: "POST",
     headers: { "Content-Type": "application/json" },
     body: JSON.stringify({ title, description }),
   });
   ```

---

### **How to Add a New Database Model**

**Example: Adding Challenges table**

1. **Edit schema**:
   ```prisma
   // prisma/schema.prisma
   
   model Challenge {
     id        String   @id @default(cuid())
     slug      String   @unique
     title     String
     description String
     difficulty String
     createdAt DateTime @default(now())
     
     userId    String
     user      User     @relation(fields: [userId], references: [id], onDelete: Cascade)
     
     @@index([userId, createdAt])
   }
   
   // Add to User model:
   model User {
     // ... existing fields
     challenges Challenge[]
   }
   ```

2. **Create migration**:
   ```bash
   npm run prisma:migrate -- --name add_challenges
   # Generates: prisma/migrations/<timestamp>_add_challenges/migration.sql
   ```

3. **Generate client**:
   ```bash
   npm run prisma:generate
   ```

4. **Use in code**:
   ```typescript
   const challenge = await prisma.challenge.create({
     data: { slug, title, description, difficulty, userId },
   });
   ```

---

### **How to Update Content (Markdown)**

1. **Push to GitHub repo**:
   ```bash
   cd ../frontend-evolution-questions-and-cheatsheets
   # Add/edit markdown files in InterviewQuestions/, etc.
   git add .
   git commit -m "Add React hooks question"
   git push origin main
   ```

2. **Webhook triggers automatically**:
   - GitHub sends webhook to `/api/revalidate`
   - Content validated
   - Index regenerated
   - Affected pages revalidated via ISR

3. **Or manually rebuild locally**:
   ```bash
   npm run validate:content
   npm run build:content-index
   npm run dev
   ```

---

### **Common Pitfalls**

**1. Forgetting to run `prisma:generate`**
- After editing schema.prisma, must regenerate client
- Symptoms: `Property 'X' not found on PrismaClient`
- Fix: `npm run prisma:generate`

**2. Session not available in client components**
- `auth()` only works in server components
- Symptoms: "auth is not a function" error
- Fix: Move to parent server component or use `useSession()` hook

**3. Circular imports**
- Importing page in component, component in page
- Symptoms: Module parse error
- Fix: Move shared logic to `lib`

**4. Modified content not showing**
- Content index cached at build time
- Symptoms: New questions don't appear
- Fix: Run `npm run build:content-index` or push to GitHub

**5. Environment variables undefined**
- .env.local not loaded in dev
- Symptoms: `process.env.DATABASE_URL is undefined`
- Fix: Ensure .env.local exists and restart dev server

---

## **TECHNICAL DEBT REPORT**

### **Critical** 🔴

**1. No Rate Limiting on Auth Endpoints**
- **File**: `route.ts`
- **Impact**: Brute force vulnerability
- **Effort**: MEDIUM (requires external service like Upstash)
- **Recommendation**: Implement ASAP before production

**2. PDF Certificates Stored in Database**
- **File**: `certificates.ts`, [src/app/api/me/study-plans/[id]/certificate/route.ts](src/app/api/me/study-plans/[id]/certificate/route.ts)
- **Impact**: Database bloat (data URLs are large)
- **Effort**: LARGE (refactor to cloud storage)
- **Recommendation**: Move to S3/Cloudflare R2

**3. Content Index Loaded on Every Request**
- **File**: `content-index.ts`
- **Impact**: Memory usage, slower requests with 500+ questions
- **Effort**: MEDIUM (implement pagination)
- **Recommendation**: Implement pagination or lazy loading

---

### **High Priority** 🟡

**1. No Email Verification**
- **File**: `route.ts`
- **Impact**: Spam accounts possible
- **Effort**: LARGE (add email queue, verification tokens)
- **Recommendation**: Before accepting user-generated content

**2. Missing CSRF Token Validation**
- **File**: All state-changing routes
- **Impact**: CSRF attack possible (mitigated by SameSite cookie)
- **Effort**: SMALL (add CSRF middleware)
- **Recommendation**: Add explicit CSRF tokens

**3. No Input Sanitization on Markdown**
- **File**: `markdown-content.tsx`
- **Impact**: XSS possible if content includes script tags
- **Effort**: SMALL (add rehype-sanitize plugin)
- **Recommendation**: Add sanitization immediately

**4. Progress Calculation Not Cached**
- **File**: src/app/(shell)/dashboard/page.tsx/dashboard/page.tsx)
- **Impact**: Dashboard loads slowly (filters entire plan items)
- **Effort**: MEDIUM (add database-level cache)
- **Recommendation**: Before scaling to 10k+ users

**5. No Search/Full-Text Indexing**
- **File**: Questions page uses client-side filtering
- **Impact**: Can't search by content, only frontend facets
- **Effort**: LARGE (add PostgreSQL FTS or Meilisearch)
- **Recommendation**: Nice-to-have but improves UX significantly

---

### **Medium Priority** 🟠

**1. Study Plan Seeding on Every Request**
- **File**: `study-plans.ts`
- **Impact**: Unnecessary DB queries
- **Effort**: SMALL (move to database initialization)
- **Recommendation**: Seed once at startup

**2. No Audit Logging**
- **File**: All API routes
- **Impact**: Can't track suspicious activity
- **Effort**: MEDIUM (add audit log table + middleware)
- **Recommendation**: Before handling sensitive user data

**3. Weak Password Requirements**
- **File**: `route.ts`
- **Impact**: Users can choose weak passwords
- **Effort**: SMALL (add regex validation)
- **Recommendation**: Encourage strong passwords

**4. Mock Data Hardcoded**
- **File**: `mock-data.ts`
- **Impact**: Difficult to update, fallback if content repo down
- **Effort**: SMALL (externalize to JSON or DB)
- **Recommendation**: Nice-to-have for maintainability

**5. No Analytics**
- **File**: N/A
- **Impact**: Can't track user behavior
- **Effort**: SMALL (add Plausible or Mixpanel)
- **Recommendation**: For business insights

---

### **Nice-to-Have** 💡

**1. Image Optimization**
- Optimize company logos, certificates
- Use Next.js `Image` component

**2. Mobile Responsiveness Testing**
- Add Playwright tests for mobile viewports

**3. Accessibility Improvements**
- ARIA labels on interactive elements
- Keyboard navigation for question filters

**4. Dark Mode Refinements**
- Optimize colors for contrast
- Add more theme options (high contrast, sepia)

**5. Offline Support**
- Service Worker for offline question reading
- Sync when online

**6. Real-Time Collaboration**
- Share progress with study partner
- Multiplayer study sessions

**7. Advanced Analytics**
- Time spent per question
- Success rates by topic
- Recommended practice areas

---

## **ARCHITECTURE DECISION RECORDS**

### **ADR 1: Server Components + Client Components Hybrid**

**Decision**: Use React Server Components (RSC) for data fetching, Client Components for interactivity

**Rationale**:
- Server components eliminate need for API layer between frontend and database
- Cleaner code: fetch data directly in page component
- Smaller JS bundles: data fetching logic stays on server
- Client components only for interactive features (forms, state)

**Pros**:
- Improved performance (less JS to browser)
- Simpler mental model (no useEffect data fetching)
- Built-in streaming support
- SEO benefits (full server-rendered HTML)

**Cons**:
- Can't use hooks like `useState` in server components
- Async/await only works in server components
- Client components can't import server components
- Learning curve for team

**Alternatives Considered**:
- Full client-side SPA (Next.js without RSC)
  - Pros: Familiar to most devs
  - Cons: Larger bundle, slower initial load, hydration mismatches
- Traditional Next.js with getServerSideProps
  - Pros: Widely known pattern
  - Cons: Less efficient, deprecated in App Router

---

### **ADR 2: JWT Session Strategy Over Database Sessions**

**Decision**: Use JWT tokens stored in httpOnly cookies instead of database sessions

**Rationale**:
- Stateless: Scale without session store
- JWT embeds user data: Fewer database queries
- Security: httpOnly prevents XSS access

**Pros**:
- Horizontal scalability (no session affinity needed)
- Self-contained auth (don't need to query session table)
- Standard (widely supported)

**Cons**:
- Can't revoke tokens immediately (until expiration)
- Slightly larger cookie size (metadata embedded)
- Need to refresh user data on each request (we do this in jwt callback)

**Alternatives Considered**:
- Database sessions
  - Pros: Easy revocation
  - Cons: Session table queries on every request
- OAuth2 Bearer tokens
  - Pros: Standard
  - Cons: Requires external OAuth provider for internal app

---

### **ADR 3: ISR (Incremental Static Regeneration) for Content Updates**

**Decision**: Statically generate question pages, revalidate via GitHub webhook on content push

**Rationale**:
- Questions rarely change (edit cycle is long)
- Static pages are fast (serve from cache)
- ISR allows on-demand regeneration without full rebuild
- GitHub webhook provides automatic trigger

**Pros**:
- Fastest possible page loads (pre-rendered HTML)
- No build required for content updates
- Automatic deployment (push → regenerate)
- CDN-friendly (static assets)

**Cons**:
- Brief period (during regeneration) where users see stale content
- Requires webhook configuration
- Complexity in handling validation failures

**Alternatives Considered**:
- Server-side rendering (SSR)
  - Pros: Always fresh
  - Cons: Slower (render on each request), requires db query per user
- Client-side rendering
  - Pros: Instant navigation
  - Cons: Larger JS bundle, no SEO, slow first paint

---

### **ADR 4: External Markdown Repository for Content**

**Decision**: Store questions in separate GitHub repository, import via API during build

**Rationale**:
- Decouples content management from application
- Enables non-technical content editors to contribute
- Version control for content
- Potential for community contributions

**Pros**:
- Content team doesn't need code access
- Separate deployment cycle for content
- Easy rollback of content changes
- Scalable (can have multiple repos by topic)

**Cons**:
- External API dependency at build time
- Network latency for validation
- Validation must pass for build to succeed
- Need to maintain webhook infrastructure

**Alternatives Considered**:
- Content in database
  - Pros: Faster queries, can be dynamic
  - Cons: Non-technical editing harder, versioning harder
- Hardcoded in codebase
  - Pros: No external dependency
  - Cons: Scales poorly, requires code deploy for content update

---

### **ADR 5: Zod for Input Validation**

**Decision**: Use Zod for runtime schema validation on all API inputs

**Rationale**:
- Runtime type safety (TypeScript alone doesn't validate at runtime)
- Clear error messages
- Reusable schemas
- Plays well with Next.js

**Pros**:
- Catches invalid inputs early
- Provides structured error responses
- Can share schema between client and server
- Composable (can combine schemas)

**Cons**:
- Bundle size (though small)
- Extra validation step (vs trust frontend)
- Boilerplate for simple endpoints

**Alternatives Considered**:
- No validation (trust frontend)
  - Pros: Fastest
  - Cons: Security risk, bad UX
- Manual validation
  - Pros: No dependency
  - Cons: Error-prone, verbose

---

### **ADR 6: Prisma ORM for Database Access**

**Decision**: Use Prisma client for all database queries

**Rationale**:
- Type-safe queries (TypeScript catches errors)
- Auto-migration system
- Multi-database support (could swap PostgreSQL later)
- Automatic relationship loading

**Pros**:
- Prevents SQL injection
- Query builder is intuitive
- Schema is single source of truth
- Good dev experience (Prisma Studio)

**Cons**:
- Slight performance overhead vs raw SQL
- Learning curve for team
- Opinionated schema design

**Alternatives Considered**:
- Raw SQL
  - Pros: Maximum performance
  - Cons: Error-prone, SQL injection risk
- TypeORM
  - Pros: Decorator-based, more like ORMs
  - Cons: More complex, larger bundle

---

## **IMPROVEMENT ROADMAP**

### **Phase 1: Security Hardening** (Weeks 1-2)
- [ ] Implement rate limiting on auth endpoints
- [ ] Add email verification flow
- [ ] Add sanitization to markdown renderer
- [ ] Make webhook signature validation required
- [ ] Implement CSRF tokens
- **Effort**: 2 weeks, **Priority**: CRITICAL

### **Phase 2: Performance Optimization** (Weeks 3-4)
- [ ] Implement pagination for questions
- [ ] Cache progress calculations at DB level
- [ ] Move PDFs to S3
- [ ] Lazy load markdown renderer
- **Effort**: 2 weeks, **Priority**: HIGH

### **Phase 3: Feature Expansion** (Weeks 5-8)
- [ ] Search/full-text indexing
- [ ] Premium features (advanced analytics, custom plans)
- [ ] Real-time progress sync (WebSocket)
- [ ] Mobile app (React Native)
- **Effort**: 4 weeks, **Priority**: MEDIUM

### **Phase 4: Scaling & Observability** (Weeks 9-12)
- [ ] Add monitoring/alerting (Datadog, Sentry)
- [ ] Implement audit logging
- [ ] Set up caching layer (Redis)
- [ ] Database query optimization
- [ ] Load testing infrastructure
- **Effort**: 4 weeks, **Priority**: HIGH (pre-launch)

---

## **RUNNING COMMON TASKS**

### **Development**
```bash
npm run dev              # Start dev server on port 3000
npm run lint            # Run ESLint
```

### **Database**
```bash
npm run prisma:generate   # Generate Prisma client after schema changes
npm run prisma:migrate    # Create/apply migrations interactively
npx prisma studio        # Open Prisma Studio (DB UI)
npx prisma migrate reset  # DESTRUCTIVE: Clear and re-seed
```

### **Content**
```bash
npm run validate:content      # Validate external content repo
npm run build:content-index   # Generate src/generated/content-index.json
```

### **Production**
```bash
npm run build            # Build for production
npm start                # Start production server
```

---

## **CONCLUSION**

**FrontendEvolution** is a well-architected, modern Next.js application designed for interview preparation. It combines server-side rendering for performance, robust authentication, and a clean separation of concerns.

**Strengths**:
- ✅ Modern tech stack (React 19, Next.js 16, TypeScript)
- ✅ Scalable architecture (ISR, server components, database-driven)
- ✅ Clean code organization (lib, components, pages)
- ✅ Good security practices (bcryptjs, JWT, Prisma, Zod validation)
- ✅ Production-ready deployment model (GitHub webhooks, ISR)

**Key Improvements Needed**:
- 🔴 Rate limiting and email verification (security)
- 🟡 Pagination for questions (performance at scale)
- 🟡 PDF externalization (database optimization)
- 🟡 Audit logging (compliance)

**For New Engineers**:
- Start by running locally (`npm run dev`)
- Review the Route Map for navigation structure
- Study `auth.ts` to understand authentication
- Explore page components to see data fetching patterns
- Check API routes for endpoint implementations

This documentation should provide everything needed to understand, maintain, and extend the project.
