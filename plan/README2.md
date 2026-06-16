# Turborepo starter

This is an official Yarn v1 starter turborepo.

## What's inside?

This turborepo uses [Yarn](https://classic.yarnpkg.com/) as a package manager. It includes the following packages/apps:

### Apps and Packages

- `docs`: a [Next.js](https://nextjs.org/) app
- `web`: another [Next.js](https://nextjs.org/) app
- `ui`: a stub React component library shared by both `web` and `docs` applications
- `eslint-config-custom`: `eslint` configurations (includes `eslint-config-next` and `eslint-config-prettier`)
- `tsconfig`: `tsconfig.json`s used throughout the monorepo

Each package/app is 100% [TypeScript](https://www.typescriptlang.org/).

### Utilities

This turborepo has some additional tools already setup for you:

- [TypeScript](https://www.typescriptlang.org/) for static type checking
- [ESLint](https://eslint.org/) for code linting
- [Prettier](https://prettier.io) for code formatting

### Build

To build all apps and packages, run the following command:

```
cd my-turborepo
yarn run build
```

### Develop

To develop all apps and packages, run the following command:

```
cd my-turborepo
yarn run dev
```

### Remote Caching

Turborepo can use a technique known as [Remote Caching](https://turbo.build/repo/docs/core-concepts/remote-caching) to share cache artifacts across machines, enabling you to share build caches with your team and CI/CD pipelines.

By default, Turborepo will cache locally. To enable Remote Caching you will need an account with Vercel. If you don't have an account you can [create one](https://vercel.com/signup), then enter the following commands:

```
cd my-turborepo
npx turbo login
```

This will authenticate the Turborepo CLI with your [Vercel account](https://vercel.com/docs/concepts/personal-accounts/overview).

Next, you can link your Turborepo to your Remote Cache by running the following command from the root of your turborepo:

```
npx turbo link
```

## Useful Links

Learn more about the power of Turborepo:

- [Tasks](https://turbo.build/repo/docs/core-concepts/monorepos/running-tasks)
- [Caching](https://turbo.build/repo/docs/core-concepts/caching)
- [Remote Caching](https://turbo.build/repo/docs/core-concepts/remote-caching)
- [Filtering](https://turbo.build/repo/docs/core-concepts/monorepos/filtering)
- [Configuration Options](https://turbo.build/repo/docs/reference/configuration)
- [CLI Usage](https://turbo.build/repo/docs/reference/command-line-reference)

# 🍺 The Event Pub

A full-stack event management application built with the **T3 Stack**. This app features a custom "Dark Pub" aesthetic, allowing users to draft event plans, manage "patrons" (guests), open a "tab" (budget), and curate a "jukebox" (Spotify playlist).

## ✨ Features

### 🔐 Authentication (The Bouncer)
* **Custom Login & Register Pages:** Themed "Open Tab" and "Join the Club" screens.
* **Google OAuth:** One-click sign-in.
* **Credentials:** Email/Password login with secure hashing.
* **Protected Routes:** Users can only manage their own events.

### 📝 Event Management (The Draft)
* **The Dashboard:** A digital menu board showing all event details.
* **The Tab (Budget):**
    * Visual progress bar showing spending vs. limit.
    * Real-time "Over Limit" alerts (turning red).
    * Itemized expense logging.
* **Bar Prep (Tasks):** Interactive checklist for event tasks.

### 🪑 Seating & Patrons
* **Patron Management:** Add and track guests via a "Guest Manifest."
* **Interactive Seating Map:**
    * Custom 4x4 grid (Tables A1-D4).
    * Transparent design allowing the pub background to show through.
    * Click-to-assign functionality.

### 🎧 Jukebox (Spotify Integration)
* **Search:** Transparent search bar powered by the **Spotify Web API**.
* **Playlist:** Add songs to the event's request list.
* **Embedded Player:** Preview tracks directly on the dashboard.

### 🧾 Closing Time (Summary)
* **Finalize Event:** Lock the event to prevent further edits ("Close Tab").
* **Invoice View:** Generates a professional "Receipt" style summary of the event.
* **Print Support:** One-click printing optimized for physical paper or PDF export.

---

## 🛠️ Tech Stack

* **Framework:** [Next.js 14](https://nextjs.org/) (App Router)
* **Language:** [TypeScript](https://www.typescriptlang.org/)
* **Database:** [PostgreSQL](https://www.postgresql.org/) (via [Neon](https://neon.tech/))
* **ORM:** [Prisma](https://www.prisma.io/)
* **Styling:** [Tailwind CSS](https://tailwindcss.com/)
* **Authentication:** [NextAuth.js](https://next-auth.js.org/)
* **Package Manager:** [pnpm](https://pnpm.io/)

---

## 🚀 Getting Started

### 1. Prerequisites
* Node.js (v18.17+ required)
* pnpm
* A PostgreSQL Database URL (Neon or local)

### 2. Installation

Clone the repository and install dependencies:

```bash
git clone <your-repo-url>
cd event-planner
pnpm install


3. Environment Variables
Create a .env file in apps/web/.env and add the following keys:


# --- DATABASE (Neon / Postgres) ---
DATABASE_URL="postgres://user:password@host/db?sslmode=require"

# --- NEXT AUTH ---
NEXTAUTH_URL="http://localhost:3000"
NEXTAUTH_SECRET="your-random-secret-string"

# --- GOOGLE AUTH (For Login) ---
GOOGLE_CLIENT_ID="your-google-client-id"
GOOGLE_CLIENT_SECRET="your-google-client-secret"

# --- SPOTIFY API (For Music Search) ---
SPOTIFY_CLIENT_ID="your-spotify-client-id"
SPOTIFY_CLIENT_SECRET="your-spotify-client-secret"


4. Database Setup
Push the schema to your database:

# Generate Prisma Client
pnpm db:generate

# Push schema to DB
pnpm db:push


5. Run the Application
Start the development server:

Bash
pnpm dev
Open http://localhost:3000 in your browser.


📄 License
Distributed under the MIT License.

---

### 📂 Files Info (Quick Reference)

Here is a summary of the critical files in your project so you know where everything is located.

#### **1. Authentication & Config**
* **`apps/web/.env`**: Stores your API keys and Database URL.
* **`apps/web/src/lib/auth.ts`**: The main Auth config. Points to the custom login page and handles the database check.
* **`apps/web/src/app/api/auth/[...nextauth]/route.ts`**: The backend engine that powers NextAuth.

#### **2. Pages (The Frontend)**
* **`apps/web/src/app/page.tsx`**: The **Home Page**. Handles the "Welcome" screen and the "Create Event" form.
* **`apps/web/src/app/login/page.tsx`**: The **Custom Login Page** (The dark form with the gold bar).
* **`apps/web/src/app/register/page.tsx`**: The **Registration Page** (The "Join the Club" form).
* **`apps/web/src/app/events/[id]/page.tsx`**: The **Main Dashboard**. Displays the 3 columns (Tab, Patrons, Jukebox).
* **`apps/web/src/app/events/[id]/summary/page.tsx`**: The **Invoice Page**. Shown after clicking "Close Tab".

#### **3. Components (The UI Parts)**
* **`apps/web/src/components/SeatMap.tsx`**: The interactive transparent seating grid.
* **`apps/web/src/components/SpotifySearch.tsx`**: The music search bar and result list.
* **`apps/web/src/components/ClearableForms.tsx`**: Contains `GuestForm`, `TaskForm`, and `ExpenseForm` (the inputs that clear themselves).
* **`apps/web/src/components/PrintButton.tsx`**: The button that triggers the print dialog.
* **`apps/web/src/components/SignOutButton.tsx`**: The dedicated button to handle sign-out logic properly.

#### **4. Backend Logic**
* **`apps/web/src/app/actions.ts`**: Contains all server functions (`createEvent`, `addGuest`, `finalizeEvent`, etc.).
* **`packages/database/prisma/schema.prisma`**: Defines your database tables (`User`, `Event`, `Guest`, `Track`, etc.).

#### **5. Styles**
* **`apps/web/tailwind.config.ts`**: Defines the custom colors (`pub-gold`, `pub-charcoal`) and the background image.
* **`apps/web/src/app/globals.css`**: Defines the custom scrollbar styles.
