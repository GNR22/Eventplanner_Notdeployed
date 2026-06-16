# 🍺 The Event Pub

A full-stack event management application built with the **T3 Stack**. This app features a custom **Dark Pub** aesthetic, allowing users to draft event plans, manage patrons (guests), open a tab (budget), and curate a jukebox (Spotify playlist).

---

# ✨ Features

## 🔐 Authentication (The Bouncer)

* Custom Login & Register Pages

  * Themed **Open Tab** and **Join the Club** screens.
* Google OAuth

  * One-click sign-in using Google.
* Credentials Authentication

  * Email and password login with secure hashing.
* Protected Routes

  * Users can only manage their own events.

---

## 📝 Event Management (The Draft)

### The Dashboard

A digital menu board displaying all event details.

### The Tab (Budget)

* Visual progress bar showing spending vs. budget limit.
* Real-time over-budget alerts.
* Itemized expense tracking.

### Bar Prep (Tasks)

* Interactive task checklist.
* Event preparation management.

---

## 🪑 Seating & Patrons

### Patron Management

* Add guests to an event.
* Track attendee information through a Guest Manifest.

### Interactive Seating Map

* Custom 4×4 seating grid (Tables A1–D4).
* Transparent design that blends with the pub theme.
* Click-to-assign guest functionality.

---

## 🎧 Jukebox (Spotify Integration)

### Spotify Search

* Search tracks using the Spotify Web API.
* Transparent themed search interface.

### Playlist Management

* Add songs to the event request list.
* Maintain a custom event playlist.

### Embedded Player

* Preview tracks directly from the dashboard.

---

## 🧾 Closing Time (Summary)

### Finalize Event

* Lock an event to prevent further edits.
* Close Tab functionality.

### Invoice View

* Professional receipt-style event summary.
* Print-friendly design.

### Print Support

* One-click printing.
* Export to PDF support.

---

# 🛠️ Tech Stack

| Category        | Technology              |
| --------------- | ----------------------- |
| Framework       | Next.js 14 (App Router) |
| Language        | TypeScript              |
| Database        | PostgreSQL (Neon)       |
| ORM             | Prisma                  |
| Styling         | Tailwind CSS            |
| Authentication  | NextAuth.js             |
| Package Manager | pnpm                    |

---

# 🚀 Getting Started

## 1. Prerequisites

Install the following:

* Node.js v18.17+
* pnpm
* PostgreSQL Database URL (Neon or Local)

---

## 2. Installation

Clone the repository and install dependencies:

```bash
git clone <your-repository-url>
cd event-planner
pnpm install
```

---

## 3. Environment Variables

Create:

```text
apps/web/.env
```

Add the following:

```env
# --- DATABASE (Neon / PostgreSQL) ---
DATABASE_URL="postgres://user:password@host/db?sslmode=require"

# --- NEXTAUTH ---
NEXTAUTH_URL="http://localhost:3000"
NEXTAUTH_SECRET="your-random-secret-string"

# --- GOOGLE AUTH ---
GOOGLE_CLIENT_ID="your-google-client-id"
GOOGLE_CLIENT_SECRET="your-google-client-secret"

# --- SPOTIFY API ---
SPOTIFY_CLIENT_ID="your-spotify-client-id"
SPOTIFY_CLIENT_SECRET="your-spotify-client-secret"
```

---

## 4. Database Setup

Generate Prisma Client:

```bash
pnpm db:generate
```

Push schema to database:

```bash
pnpm db:push
```

Verify database:

```bash
pnpm db:studio
```

Prisma Studio will open:

```text
http://localhost:5555
```

---

## 5. Run the Application

Start development server:

```bash
pnpm dev
```

Open:

```text
http://localhost:3000
```

---

# 🗄️ Neon Database Setup

## Step 1: Create a Neon Project

1. Create an account at Neon.
2. Click **New Project**.
3. Enter project name:

   * Example: `event-planner`
4. Select your preferred region.
5. Leave PostgreSQL version as default.
6. Click **Create Project**.

---

## Step 2: Obtain Connection String

1. Open Neon Dashboard.
2. Navigate to **Connection Details**.
3. Select the Prisma connection option if available.
4. Disable **Pooled Connection** for local development.
5. Copy the connection string.

Example:

```env
postgres://user:password@host/database?sslmode=require
```

---

## Step 3: Configure Environment File

Open:

```text
apps/web/.env
```

Set:

```env
DATABASE_URL="postgres://user:password@host/database?sslmode=require"
```

---

## Step 4: Create Database Tables

Generate Prisma Client:

```bash
pnpm db:generate
```

Push Schema:

```bash
pnpm db:push
```

---

## Step 5: Verify Database

Launch Prisma Studio:

```bash
pnpm db:studio
```

If you see tables such as:

* User
* Event
* Guest
* Track

your database is configured correctly.

---

# 🧹 Dependency Repair Guide

If you encounter errors such as:

```text
MODULE_NOT_FOUND
globby not found
styled-jsx not found
cross-spawn not found
```

perform a clean installation.

## Clean Project

Linux/macOS:

```bash
rm -rf node_modules
rm -rf pnpm-lock.yaml
rm -rf .next
```

Windows:

Delete manually:

* node_modules
* pnpm-lock.yaml
* .next

---

## Reinstall Dependencies

```bash
pnpm install
```

---

## Regenerate Prisma Client

```bash
pnpm db:generate
```

---

## Push Schema

```bash
pnpm db:push
```

---

## Start Development Server

```bash
pnpm dev
```

---

# ⚠️ OneDrive Warning

Avoid storing Node.js projects inside OneDrive.

Example problematic location:

```text
C:\Users\<username>\OneDrive\
```

Recommended locations:

```text
C:\Projects\event-planner
```

or

```text
C:\Users\<username>\Projects\event-planner
```

OneDrive may:

* Lock files.
* Remove files using Files On-Demand.
* Corrupt node_modules.
* Cause missing package errors.

---

# 🔧 Port Troubleshooting

If port 3000 is occupied:

Kill Node.js processes:

```cmd
taskkill /F /IM node.exe
```

Then restart:

```bash
pnpm dev
```

Open:

```text
http://localhost:3000
```

---

# 📂 Project Structure & File Reference

## Authentication & Configuration

### apps/web/.env

Stores:

* Database URL
* OAuth Keys
* Secrets

### apps/web/src/lib/auth.ts

Main NextAuth configuration.

### apps/web/src/app/api/auth/[...nextauth]/route.ts

NextAuth API route handler.

---

## Frontend Pages

### apps/web/src/app/page.tsx

Home page.

Displays:

* Welcome screen
* Create Event form

### apps/web/src/app/login/page.tsx

Custom login page.

### apps/web/src/app/register/page.tsx

Registration page.

### apps/web/src/app/events/[id]/page.tsx

Main dashboard.

Contains:

* Budget
* Guests
* Spotify playlist

### apps/web/src/app/events/[id]/summary/page.tsx

Invoice / Receipt page.

Optimized for printing.

---

## Components

### apps/web/src/components/SeatMap.tsx

Interactive seating grid.

### apps/web/src/components/SpotifySearch.tsx

Spotify search interface.

### apps/web/src/components/ClearableForms.tsx

Contains:

* GuestForm
* ExpenseForm
* TaskForm

Inputs automatically clear after submission.

### apps/web/src/components/SignOutButton.tsx

Handles logout functionality.

### apps/web/src/components/PrintButton.tsx

Handles printing functionality.

---

## Layout & Styling

### apps/web/src/app/layout.tsx

Global layout wrapper.

Applies:

* Background texture
* Global theme
* White text color

### apps/web/tailwind.config.ts

Defines custom theme colors:

* pub-gold
* pub-charcoal
* pub-wood

### apps/web/src/app/globals.css

Global styling and custom scrollbar.

---

## Backend Logic

### apps/web/src/app/actions.ts

Contains server actions:

* createEvent()
* addGuest()
* addExpense()
* addTask()
* finalizeEvent()

### packages/database/prisma/schema.prisma

Database schema definitions:

* User
* Event
* Guest
* Track
* Expense
* Task

---

# 🗃️ SQL

> Insert your SQL scripts, queries, migrations, and notes here.

```sql
-- -- db name: eventplanner
-- 1. Create NextAuth Tables (Quoted Names)
CREATE TABLE "User" (
    id TEXT NOT NULL PRIMARY KEY,
    name TEXT,
    email TEXT UNIQUE,
    "emailVerified" TIMESTAMP(3),
    image TEXT,
    password TEXT
);

CREATE TABLE "Account" (
    id TEXT NOT NULL PRIMARY KEY,
    "userId" TEXT NOT NULL REFERENCES "User"(id) ON DELETE CASCADE ON UPDATE CASCADE,
    type TEXT NOT NULL,
    provider TEXT NOT NULL,
    "providerAccountId" TEXT NOT NULL,
    refresh_token TEXT,
    access_token TEXT,
    expires_at INTEGER,
    token_type TEXT,
    scope TEXT,
    id_token TEXT,
    session_state TEXT,
    UNIQUE(provider, "providerAccountId")
);

CREATE TABLE "Session" (
    id TEXT NOT NULL PRIMARY KEY,
    "sessionToken" TEXT NOT NULL UNIQUE,
    "userId" TEXT NOT NULL REFERENCES "User"(id) ON DELETE CASCADE ON UPDATE CASCADE,
    expires TIMESTAMP(3) NOT NULL
);

CREATE TABLE "VerificationToken" (
    identifier TEXT NOT NULL,
    token TEXT NOT NULL UNIQUE,
    expires TIMESTAMP(3) NOT NULL,
    UNIQUE(identifier, token)
);

-- 2. Create App Tables (Lowercase Names, Mixed Columns)

CREATE TABLE event (
    id SERIAL PRIMARY KEY,
    name TEXT NOT NULL,
    budget_limit DOUBLE PRECISION DEFAULT 0 NOT NULL,
    event_date TIMESTAMP(3),
    location TEXT,
    status TEXT DEFAULT 'PLANNING' NOT NULL,
    created_at TIMESTAMP(3) DEFAULT CURRENT_TIMESTAMP NOT NULL,
    updated_at TIMESTAMP(3) NOT NULL,
    
    -- Note: snake_case column
    owner_id TEXT NOT NULL REFERENCES "User"(id) ON DELETE CASCADE ON UPDATE CASCADE
);

CREATE TABLE guest (
    id SERIAL PRIMARY KEY,
    name TEXT NOT NULL,
    status TEXT DEFAULT 'invited' NOT NULL,
    seat_number TEXT,
    
    -- Note: quoted "eventId" column
    "eventId" INTEGER NOT NULL REFERENCES event(id) ON DELETE CASCADE ON UPDATE CASCADE
);

CREATE TABLE task (
    id SERIAL PRIMARY KEY,
    title TEXT NOT NULL,
    
    -- Note: quoted "isDone" column
    "isDone" BOOLEAN DEFAULT false NOT NULL,
    
    -- Note: quoted "eventId" column
    "eventId" INTEGER NOT NULL REFERENCES event(id) ON DELETE CASCADE ON UPDATE CASCADE
);

CREATE TABLE expense (
    id SERIAL PRIMARY KEY,
    item TEXT NOT NULL,
    cost DOUBLE PRECISION NOT NULL,
    
    -- Note: quoted "eventId" column
    "eventId" INTEGER NOT NULL REFERENCES event(id) ON DELETE CASCADE ON UPDATE CASCADE
);

CREATE TABLE track (
    id SERIAL PRIMARY KEY,
    title TEXT NOT NULL,
    artist TEXT NOT NULL,
    spotify_id TEXT NOT NULL,
    album_art TEXT,
    
    -- Note: quoted "eventId" column
    "eventId" INTEGER NOT NULL REFERENCES event(id) ON DELETE CASCADE ON UPDATE CASCADE
);

-- 3. Create Indexes for Performance (Recommended for NextAuth)
CREATE INDEX "Account_userId_idx" ON "Account"("userId");
CREATE INDEX "Session_userId_idx" ON "Session"("userId");
```

---

# 📄 License

Distributed under the MIT License.
