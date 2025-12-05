# StarConnect CMS Implementation Plan

## Goal Description
Develop "StarConnect CMS", a comprehensive platform for the Nuit de l'Info challenge. The system will enable users to manage content, customize profiles, monetize their work, and handle crisis communication effectively.

## User Review Required
> [!IMPORTANT]
> **Tech Stack Selection**: We will use **Next.js 14+ (App Router)**, **TypeScript**, **Tailwind CSS**, **Prisma** (ORM), and **PostgreSQL** (Database). Authentication will be handled by **NextAuth.js**.
> **Database**: A local PostgreSQL instance is assumed. If not available, we will use SQLite for development speed, but PostgreSQL is preferred for production readiness. *Plan assumes SQLite for immediate local setup unless otherwise specified, but code will be Postgres-compatible.*

## Proposed Changes

### Project Structure
- **Framework**: Next.js (Fullstack)
- **Styling**: Tailwind CSS + Shadcn/UI (for rapid, premium UI components)
- **Database**: Prisma Schema

### Core Components

#### [NEW] Database Schema (`schema.prisma`)
- `User`: Profiles, Auth info, Roles
- `Content`: Articles, Videos, Galleries
- `Subscription`: Monetization tiers
- `CrisisSettings`: User-specific crisis configurations
- `Analytics`: Basic tracking data

#### [NEW] Authentication
- NextAuth configuration with Email/Password and potentially OAuth providers.

#### [NEW] CMS Dashboard (`/app/dashboard`)
- Layout with sidebar navigation.
- Pages for managing Posts, Media, Settings, Analytics.

#### [NEW] Public Profiles (`/app/[username]`)
- Dynamic route rendering user's public page.
- Custom styling based on user preferences (stored in DB).

#### [NEW] Crisis Tools (`/app/dashboard/crisis`)
- Interface to activate "Crisis Mode".
- Editor for Official Statements.

### Monetization & Social
- Integration of mock payment flows.
- Social media metadata management.

## Verification Plan

### Automated Tests
- `npm run lint`: Ensure code quality.
- `npm run build`: Verify production build succeeds.

### Manual Verification
- **Auth Flow**: Register, Login, Logout.
- **CMS Operations**: Create/Edit/Delete an article.
- **Public View**: Verify profile renders correctly and customization applies.
- **Crisis Mode**: Activate and verify public profile change.
