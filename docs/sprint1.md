# 🚀 Sprint 1 Plan — VibeReads

## 📅 Sprint Duration

Week 1–2 · March 23 – April 4, 2026

---

## 🎯 Sprint Goal

**PM & Frontend Initialization** — Establish the full product foundation and get the frontend running end-to-end with a real homepage users can interact with.

By the end of this sprint:
- All Milestone 1 PM deliverables are signed off and submitted
- The Next.js project is scaffolded, styled, and deployed with the design system in place
- The app has a working routing shell, shared component library, state infrastructure, and a live Homepage
- The team is unblocked to build all remaining pages in Sprint 2

---

## 📦 Sprint Scope

### Product Management (PM-1 through PM-6) — ✅ Completed

All six PM deliverables were completed during the first week as part of the Milestone 1 submission on March 27.

| ID | Deliverable | Owner | Status |
|---|---|---|---|
| PM-1 | Product Definition Document | Samir | ✅ Done |
| PM-2 | MVP Scope & User Story Map (MoSCoW + RICE) | Full Team | ✅ Done |
| PM-3 | Product Backlog (Linear / GitHub Issues) | Full Team | ✅ Done |
| PM-4 | Initial Wireframes (9 screens in Figma) | Samir | ✅ Done |
| PM-5 | PRD Section | Samir | ✅ Done |
| PM-6 | AI Log Entry #1 | Full Team | ✅ Done |

---

### Frontend Tasks (FE-01 through FE-07)

| ID | Task | Owner | Story Points |
|---|---|---|---|
| FE-01 | Scaffold Next.js 15 project with TypeScript strict mode | Samir | 2 |
| FE-02 | Configure Tailwind CSS design system and global theme | Samir | 3 |
| FE-03 | Implement root layout, navigation bar, and all route stubs | Samir | 3 |
| FE-04 | Build shared component library (BookCard, StarRating, ReviewCard, SearchBar, Avatar, Badge, Skeleton) | Samir | 8 |
| FE-05 | Build WantToReadButton shared component with optimistic state | Samir | 3 |
| FE-06 | Set up Zustand stores and TanStack Query infrastructure | Samir | 5 |
| FE-07 | Build Homepage page | Samir | 5 |

**Frontend Story Points: 29**

---

## 📊 Total Story Points: 29 (frontend only — PM tasks counted separately)

---

## 👥 Team Responsibilities

| Member | Sprint 1 Focus |
|---|---|
| Samir Sahiti | All FE-01 through FE-07. PM lead (PM-1 through PM-6 already delivered). |
| Fisnik Percuku | Backend architecture planning, API contract design for M3, reviewing FE API contracts |
| Yllka Nuredini | Docker Compose planning, infrastructure setup for M4, reviewing frontend deployment needs |

Fisnik and Yllka are not coding during this sprint — they are unblocked to plan their own milestone work in parallel while Samir completes the frontend foundation.

---

## 🧩 Task Breakdown

### FE-01 — Scaffold Next.js 15 project

**Owner:** Samir · **Points:** 2

- `npx create-next-app@latest` with App Router, TypeScript, Tailwind, ESLint
- Enable `strict: true` in `tsconfig.json` — no `any` types permitted
- Configure path aliases: `@/components`, `@/lib`, `@/store`, `@/hooks`, `@/types`
- Set up ESLint with `eslint-config-next` + `@typescript-eslint` + `eslint-plugin-react-hooks`
- Set up Prettier with `prettier-plugin-tailwindcss` for class sorting
- Install all M2 dependencies: `framer-motion`, `zustand`, `@tanstack/react-query`, `react-hook-form`, `zod`, `sonner`, `lucide-react`, `recharts`, `clsx`, `tailwind-merge`
- CI: add a `.github/workflows/ci.yml` that runs `npm run lint` and `npm run build` on every push to `main` and every PR

---

### FE-02 — Configure Tailwind CSS design system and global theme

**Owner:** Samir · **Points:** 3

- Extend `tailwind.config.ts` with the full `vibeColors` map (8 moods × bg/text/border)
- Add custom `fontFamily` using the Geist font stack (via `next/font`)
- Define CSS custom properties in `app/globals.css` (`--brand-primary`, `--brand-gradient`, `--card-border`, `--card-radius`)
- Mount `<Toaster />` from Sonner in root `app/layout.tsx`
- Add `lib/utils.ts` with the `cn()` helper (`clsx` + `tailwind-merge`)
- Set dark mode strategy to `class` in Tailwind config (toggle-ready, even if toggle UI isn't built yet)

---

### FE-03 — Implement root layout, navbar, and route stubs

**Owner:** Samir · **Points:** 3

- Build `components/layout/Navbar.tsx`: sticky, desktop nav links + mobile hamburger
- Active link detection via `usePathname()`
- Create all 9 route stubs with placeholder content and correct `metadata` exports
- Apply `min-h-screen bg-gray-50` to body wrapper in root layout

---

### FE-04 — Build shared component library

**Owner:** Samir · **Points:** 8

- `BookCard` (3 variants: default, compact, horizontal)
- `StarRating` (display + interactive modes)
- `ReviewCard` (with spoiler toggle)
- `SearchBar` (default + hero sizes)
- `Avatar` (4 sizes, image + fallback)
- `Badge` (vibe, genre, status, difficulty variants)
- `Skeleton` family: `SkeletonBookCard`, `SkeletonReviewCard`, `SkeletonText`

---

### FE-05 — Build WantToReadButton

**Owner:** Samir · **Points:** 3

- Default and compact variants
- Optimistic toggle (Zustand update before API resolves)
- Error rollback
- `e.stopPropagation()` to prevent card link navigation on click

---

### FE-06 — Set up state management infrastructure

**Owner:** Samir · **Points:** 5

- `QueryClient` singleton with defaults + `QueryClientProvider` in root layout
- `ReactQueryDevtools` (dev only, dynamic import)
- `store/readingListStore.ts` (Zustand + localStorage persist)
- `store/uiStore.ts` (ephemeral UI state — filters, search query, notifications)
- `store/moodProfileStore.ts` (Zustand + localStorage persist)
- `lib/api/mockReadingList.ts` — async mock functions with 300ms delay + 10% error rate
- `hooks/useReadingList.ts` — full TanStack Query hooks with optimistic updates
- `hooks/useMoodProfile.ts` — full TanStack Query hooks, 5% error rate, 2 retries

---

### FE-07 — Build Homepage

**Owner:** Samir · **Points:** 5

- Hero section: gradient, search bar (hero size), 4–5 vibe tag pills, "Start Discovering" CTA
- Trending This Week: 6-book responsive grid with `SkeletonBookCard` loading state
- Featured Collections: 3-column card grid
- Quick Actions: 2×2 action tile grid
- SSR page (no `'use client'`) with exported `metadata`

---

## ✅ Definition of Done

Sprint 1 is complete when:

- All PM-1 through PM-6 deliverables submitted and signed off (already done ✅)
- `npm run build` passes with zero TypeScript errors and zero ESLint warnings
- CI pipeline is green on `main`
- All 9 route stubs are reachable without a 404
- Homepage renders all 4 sections with correct styling on desktop and mobile
- Reading list optimistic update works: add a book on the homepage, see it instantly toggle — and see it roll back on the simulated error
- `docs/ai-log.md` Entry #2 started (in progress, completed at end of Sprint 2)

---

## ⚠️ Risks & Mitigation

| Risk | Mitigation |
|---|---|
| FE-04 takes longer than estimated — 7 components is a lot for one task | If falling behind by Day 5, deprioritise `SkeletonReviewCard` and `Avatar` (used less) and do them at the start of Sprint 2 |
| WantToReadButton optimistic rollback is tricky to get right | Test the 10% error rate manually and write the RTL test before considering it done |
| Zustand persist middleware can cause hydration mismatches in Next.js SSR | Use `skipHydration: true` on the persist config and manually rehydrate on the client with `useEffect` |

---

## 📌 Notes

FE-01 through FE-06 are pure infrastructure — no visible UI until FE-07 lands. That's intentional. A solid foundation here means Sprint 2 pages go up fast.

The sprint is slightly front-loaded for Samir. Fisnik and Yllka should use this time to fully plan M3 and M4 respectively so they're ready to hit the ground running in Sprint 3.
