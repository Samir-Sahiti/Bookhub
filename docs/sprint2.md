# 🚀 Sprint 2 Plan — VibeReads

## 📅 Sprint Duration

Week 3–4 · April 5 – April 17, 2026

---

## 🎯 Sprint Goal

**Frontend MVP — Complete** — Ship every remaining frontend page, animation layer, tests, and documentation so that Milestone 2 is fully deliverable by April 17.

By the end of this sprint:
- All 9 pages are built and navigable
- Animations are wired up across the full app
- Jest + RTL unit tests and Playwright e2e tests are passing in CI
- Accessibility audit is complete with zero Critical/Serious violations
- Lighthouse performance report is written
- `.cursorrules` is configured and AI Log Entry #2 is complete

---

## 📦 Sprint Scope — FE-08 through FE-20

| ID | Task | Owner | Points | Priority |
|---|---|---|---|---|
| FE-08 | Build Vibe Search page with filters and results grid | Samir | 5 | Must Have |
| FE-09 | Build Book Detail page | Samir | 5 | Must Have |
| FE-10 | Build multi-step Review Submission wizard | Samir | 8 | Must Have |
| FE-11 | Build Create Reading Club form | Samir | 5 | Could Have |
| FE-12 | Build Writer Hub dashboard UI | Samir | 5 | Could Have |
| FE-13 | Build Reading Challenges discovery page | Samir | 5 | Could Have |
| FE-14 | Build 5-step Mood Profile Builder | Samir | 5 | Could Have |
| FE-15 | Build Mood Profile page with 5-tab layout | Samir | 8 | Could Have |
| FE-16 | Add Framer Motion animations and page transitions | Samir | 3 | Should Have |
| FE-17 | Write frontend tests (Jest + RTL + Playwright) | Samir | 5 | Must Have |
| FE-18 | Accessibility audit and fixes | Samir | 3 | Must Have |
| FE-19 | Lighthouse performance baseline and bundle optimisation | Samir | 3 | Must Have |
| FE-20 | Configure .cursorrules and document AI development workflow | Samir | 2 | Must Have |

**Total Story Points: 67**

---

## 👥 Team Responsibilities

| Member | Sprint 2 Focus |
|---|---|
| Samir Sahiti | All FE-08 through FE-20. Primary owner of the entire frontend. |
| Fisnik Percuku | Complete M3 backend plan, begin API scaffolding (.NET project setup, EF Core migrations, auth) — running in parallel |
| Yllka Nuredini | Complete Docker Compose full-stack config, begin Dockerfile authoring — running in parallel |

---

## 🗓️ Suggested Day-by-Day Pacing

Milestone 2 is due **Thursday April 17**. That gives 13 days from April 5. Below is a realistic pacing guide to avoid the classic "left testing until the last day" problem.

| Days | Tasks | Notes |
|---|---|---|
| Apr 5–6 | FE-08 (Vibe Search), FE-09 (Book Detail) | Both share BookCard + SearchBar from Sprint 1. Back-to-back makes sense. |
| Apr 7–8 | FE-10 (Review Submission wizard) | Most complex form in the app. Give it 2 full days. |
| Apr 9–10 | FE-11 (Create Club), FE-12 (Writer Hub) | Could Have. Don't gold-plate — the live preview sidebar in FE-11 can be cut if time pressure hits. |
| Apr 11–12 | FE-13 (Challenges), FE-14 (Mood Profile Builder) | Could Have. FE-14 wizard reuses patterns from FE-10, so it should go faster. |
| Apr 13 | FE-15 (Mood Profile page, 5-tab layout) | Largest single page. Recharts chart and custom vibe bar chart are the trickiest parts. |
| Apr 14 | FE-16 (Framer Motion animations) | Thread animations through all pages. Fast if PageTransition wrapper is done first. |
| Apr 15 | FE-17 (Tests — Jest + RTL + Playwright) | Unit tests for components and hooks. Playwright e2e for main happy path only. |
| Apr 16 | FE-18 (Accessibility), FE-19 (Lighthouse) | axe audit + contrast fixes. Lighthouse run + dynamic import for Recharts. |
| Apr 17 | FE-20 (.cursorrules + AI Log), final checks | Commit .cursorrules, complete AI Log Entry #2. Full CI build. Tag `milestone-2`. |

---

## 🧩 Task Breakdown

### FE-08 — Vibe Search page

**Owner:** Samir · **Points:** 5

- `'use client'` page reading `?q=` and `?vibe=` from URL params on mount
- `useDebounce(value, 400)` hook for search input — implement in `hooks/useDebounce.ts`
- URL params update on filter/search change via `router.replace` (not `router.push`) so back button works
- 10 toggleable vibe pills (emoji + label), multi-select, synced with `uiStore.activeVibeFilters`
- "Clear all" link visible when ≥1 filter active
- Client-side filter: match on vibe AND title/author text search
- Empty state: `SearchX` icon, "No books match that vibe", clear filters button
- 12 books total in mock data (6 from homepage + 6 new titles)
- 6 `SkeletonBookCard` loading state while mock data "loads"

---

### FE-09 — Book Detail page

**Owner:** Samir · **Points:** 5

- SSR page with `generateMetadata` returning book title + description for SEO
- 3-column desktop layout (cover + icon buttons left, book info spanning 2 cols right)
- "Read more" toggle for long descriptions (first 300 chars, expand on click)
- `WantToReadButton` default variant
- "Similar Vibes" grid: 4 `BookCard` compact variant
- "Reader Reviews" section: 3 `ReviewCard` components, "Write a Review" button pre-populating `?book={id}`
- Simulated live review toast: `useEffect` firing after 8 seconds (demonstrates SignalR readiness for M3)

---

### FE-10 — Review Submission wizard

**Owner:** Samir · **Points:** 8

- `useReducer` for all form state (not multiple `useState`)
- Persistent progress bar: `Step X of 4`, percentage fill, `transition-all duration-300`
- Step 1: book dropdown (pre-selected via `?book=` query param) + interactive `StarRating` (`w-12 h-12`)
- Step 2: textarea with live character counter, amber/red border at 800/900 chars, "Review tips" accordion
- Step 3: spoiler toggle (`role="switch"`, `aria-checked`), predefined tag pills + custom tag input (max 5 tags)
- Step 4: read-only preview with "Edit" jump-links back to specific steps
- Rate limiting: `localStorage['review_submissions']` → `{ count, resetAt }` — error toast if count ≥ 10
- Success screen: `CheckCircle2` scale animation, two CTA buttons

---

### FE-11 — Create Reading Club form

**Owner:** Samir · **Points:** 5

- React Hook Form + Zod validation (name min 3, book required, dates cross-validated)
- Live sidebar preview card updating as user types (can cut this if time is short)
- Book search: real-time dropdown filtering mock book list (max 5 results)
- Visibility radio cards (Public / Private) with icon + description
- Discussion format radio cards (Async / Video / Both)
- Interest tags input (same component as review tags, max 5)
- Zod schema with `.refine()` for end-date-after-start-date cross-field rule

---

### FE-12 — Writer Hub dashboard UI

**Owner:** Samir · **Points:** 5

- Purple-to-indigo hero banner, CTA buttons show "Coming soon" toast
- 4 stat cards with `useCountUp` hook (numbers animate from 0 on mount)
- Empty state for "Your Books" — one draft stub card is fine for visual completeness
- Recharts `BarChart` with 7 days of mocked view data, indigo fill
- 3 mock `ReviewCard` components as "Reader Feedback Preview"

---

### FE-13 — Reading Challenges discovery page

**Owner:** Samir · **Points:** 5

- Amber-to-orange hero banner with `Trophy` icon
- 1 mock active challenge card with animated progress bar (Framer Motion width animation on mount)
- 4 featured challenge cards — "Join" toggles to "Joined ✓" green state locally via `useState`
- Difficulty + Duration filter pills, client-side filter update
- Leaderboard teaser: top 5 rows with rank, avatar initials, username, books completed

---

### FE-14 — Mood Profile Builder (5-step wizard)

**Owner:** Samir · **Points:** 5

- `useReducer` for state (same pattern as FE-10)
- Loads existing profile via `useMoodProfileQuery()` and pre-fills all steps on mount
- Step 1: 8 mood cards (2-col grid), 1–5 rating circles, mood-specific bg colors, min 3 required
- Step 2: 14 genre pills, min 2 required
- Step 3: 15 theme pills, min 3 required
- Step 4: 3 reading pace selector cards (single-select, default "moderate")
- Step 5: 3 content preference categories (Violence / Romance / Humor), 3 options each
- Sticky footer: Back/Cancel left, Next/Complete right, disabled when validation fails
- Submit: `useSaveMoodProfile()` → success toast → 1.5s delay → navigate to `/profile`

---

### FE-15 — Mood Profile page (5-tab layout)

**Owner:** Samir · **Points:** 8

- Gradient profile header always visible: avatar, name, handle, 3 stats badges, bio block, 3 action icon buttons
- Tab state synced to URL hash (`#overview`, `#vibes`, `#stats`, `#reading-list`, `#mood-profile`) so refresh preserves the active tab
- **Tab 1 Overview:** Currently Reading (2 books + progress bars), Favourite Books grid (4 compact cards), Reading Personality traits (3 cards), Recent Activity timeline (5 events)
- **Tab 2 Vibes:** Custom CSS horizontal bar chart — 8 mood bars with mood-specific colors (no Recharts here, plain Tailwind), insight text card
- **Tab 3 Stats:** 6 stat cards with `useCountUp`, Recharts `LineChart` for books/month last 12 months
- **Tab 4 Reading List:** `useReadingListQuery()`, grid with `BookCard` default + `WantToReadButton`, empty state + summary bar
- **Tab 5 Mood Profile:** Three states — loading spinner / empty prompt → `/profile/setup` / populated (mood cards, genre pills, theme pills, content pref grid, 3 recommended books)

---

### FE-16 — Framer Motion animations

**Owner:** Samir · **Points:** 3

- `components/layout/PageTransition.tsx`: `AnimatePresence` + `motion.div`, opacity + y-offset, 200ms
- Skeleton pulse: replace Tailwind `animate-pulse` with Framer Motion opacity loop (`repeat: Infinity`, 1.5s)
- `BookCard` entrance: staggered `scale + opacity` with `delay: index * 0.05`
- Review wizard success screen: `CheckCircle2` spring scale animation
- Wizard step transitions: slide direction based on `direction` state (`x: 20` forward, `x: -20` back)
- Challenge progress bar: `motion.div` width animation from `0%` to target on mount
- Mood Profile tabs: `AnimatePresence` fade only (no slide — avoids layout shift)

---

### FE-17 — Frontend tests

**Owner:** Samir · **Points:** 5

**Setup:** `jest.config.ts` with `next/jest`, `@testing-library/jest-dom` in `jest.setup.ts`, manual mock for `next/navigation` in `__mocks__/`

**Unit tests (Jest + RTL):**
- `BookCard`: renders title/author, no nested `<a>`, snapshot, WantToReadButton present when prop set
- `StarRating`: display rounding (3.5 shows half star), interactive callback, Space key fires `onRate`
- `WantToReadButton`: default state, toggled state, loading state, rollback on error
- `useReadingList`: add, remove, optimistic update visible before mock resolves
- `ReviewSubmission`: step 1 Next disabled without rating, step 2 disabled under 50 chars, rate limit toast

**E2E (Playwright):**
- `discovery-to-review.spec.ts`: homepage → search → book detail → want to read → write review → 4 steps → success screen
- `mood-profile.spec.ts`: profile setup wizard (all 5 steps) → submit → profile page → mood-profile tab shows saved data
- `navigation.spec.ts`: all navbar links navigate correctly, mobile hamburger opens/closes

---

### FE-18 — Accessibility audit and fixes

**Owner:** Samir · **Points:** 3

- axe DevTools audit across all 9 pages — document every finding
- Fix `text-indigo-200` contrast issue on gradient backgrounds
- Add `aria-label` to all icon-only buttons (hamburger, heart, share, BookOpen, stat icons)
- Focus management in step wizards: `stepRef.current?.focus()` on step change
- "Skip to main content" link as first body child, visible on focus
- Spoiler toggle: `role="switch"` + `aria-checked`
- Form errors linked via `aria-describedby`
- Vibe pills respond to `Enter` and `Space` keydown
- Deliverable: `docs/accessibility-report.md` with violation table + fix applied per page

---

### FE-19 — Performance baseline and bundle optimisation

**Owner:** Samir · **Points:** 3

- Lighthouse audit on 4 pages: Homepage, Vibe Search, Book Detail, Mood Profile Builder (simulated mobile throttling)
- Dynamic import for Recharts in Writer Hub and Mood Profile Stats: `dynamic(() => import(...), { ssr: false })`
- `React.memo` on `BookCard` and `ReviewCard`
- `useMemo` for client-side filter logic in Vibe Search
- Add `@next/bundle-analyzer`, run `ANALYZE=true next build`, screenshot result
- `useReportWebVitals` hooked up in root layout (logs LCP/CLS/FID to console in dev — plumbed to PostHog in M6)
- Deliverable: `docs/performance-report.md` with score table + bundle screenshot + notes column

---

### FE-20 — .cursorrules and AI Log Entry #2

**Owner:** Samir · **Points:** 2

- Commit `.cursorrules` to repo root — full project context: stack, file conventions, coding rules, design system tokens, what NOT to generate
- Verify `cn()` utility used throughout (no string template class concatenation)
- Complete `docs/ai-log.md` Entry #2:
  - Components scaffolded with Cursor vs written by hand
  - Zod schemas generated by Claude vs written manually
  - Playwright tests generated by AI
  - Top 3 prompts verbatim (copy/paste)
  - Total estimated hours saved across Sprint 2
  - Examples of AI-generated code that was wrong and needed manual correction (required — instructors expect critical evaluation)

---

## ✅ Definition of Done

Sprint 2 / Milestone 2 is complete when:

- All 9 pages render without TypeScript errors on `npm run build`
- CI pipeline is green (lint + type-check + tests + build)
- `npm run test` passes with ≥ 70% coverage on hooks and core components
- Playwright e2e tests pass headless in CI
- `docs/accessibility-report.md` submitted — zero Critical/Serious axe violations
- `docs/performance-report.md` submitted — Lighthouse scores for 4 pages
- Recharts dynamically imported (not in initial bundle)
- `.cursorrules` committed to repo root
- `docs/ai-log.md` Entry #2 complete
- Repo tagged `milestone-2` with CI green at time of tagging

---

## ⚠️ Risks & Mitigation

| Risk | Mitigation |
|---|---|
| 67 story points is aggressive for one person in 13 days | Could Have pages (FE-11 through FE-15) are lower priority. If pacing slips, FE-11 (Create Club) can shift to Sprint 3 without blocking M2 grading |
| Mood Profile page (FE-15) is the most complex single page in the app | Start it on Apr 13 with the full day. If time is short, cut the Recharts chart from Tab 3 and use static numbers |
| Playwright e2e tests are slow to write | Write happy path only — edge cases belong in RTL unit tests, not e2e |
| Framer Motion hydration issues in Next.js App Router | Always use `motion` components inside `'use client'` boundaries. Never animate a Server Component directly |
| Bundle analyser reveals an unexpected large package | Dynamic import is the fix. Identify first, then apply — don't pre-optimise guesswork |

---

## 📌 Notes

Sprint 2 completes **Milestone 2 — Frontend MVP** (15% of final grade, due April 17).

After this sprint the frontend is feature-complete for both MVP and Phase 2 features. From Sprint 3 onwards, Fisnik (backend) and Yllka (DevOps) take over as primary owners and Samir shifts to support, API wiring, and analytics work in M6.

Tag `milestone-2` and push it before midnight on April 17. CI must be green at the tag commit.
