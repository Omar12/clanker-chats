# Mid-level Coding Interview

Here’s a tight, one-hour technical interview plan you can *drive as the interviewee*. It balances coding, React knowledge, and practical engineering judgment—plus strong questions for you to ask.

## 60-Minute Agenda (you lead the pacing)

**0–5 min — Context setup**

* Goal: clarify problem scope & expectations.
* Actions: restate requirements, confirm constraints (env, libs, tests, TypeScript, API availability), agree on success criteria (working path > perfect polish).

**5–25 min — Core coding exercise**

* Typical prompts: build a small interactive component (search/filter list, pagination, form with validation) or transform data → UI.
* What to show:

  * Component structure: split presentational vs. container concerns.
  * State model: colocate state, choose `useState` vs `useReducer`, lift state only when needed.
  * Data flow: controlled components, prop drilling vs context.
  * Accessibility as-you-go (labels, roles, focus order).
  * Tests: outline RTL test cases even if you can’t implement all.

**25–35 min — Debugging & extension**

* Add a feature or fix a performance bug.
* Demonstrate: reasoning, breakpoints/console, invariants, prop/state audit, binary search of the issue area.
* Perf ideas to mention: memoization (`React.memo`, `useMemo`, `useCallback`), list virtualization, key usage, lazy routes/components.

**35–45 min — React & Frontend knowledge Q&A (you answer)**
Hit concise, practical answers:

* **Hooks & state**

  * When `useReducer` > `useState`.
  * Stale closures & how to avoid them.
  * Derived state & avoiding duplication.
* **Reconciliation & rendering**

  * Why keys matter and pitfalls (index keys in mutated lists).
  * Server Components vs Client Components (when/why), Suspense basics.
* **Data fetching**

  * Fetch patterns: `useEffect` pitfalls, cancellation, React Query (cache, staleTime), error boundaries.
* **Performance**

  * Re-render sources, memo boundaries, expensive calc isolation, bundle splitting.
* **Accessibility**

  * Keyboard support, focus management (portals/modals), ARIA patterns, color contrast.
* **Testing**

  * RTL philosophy: test behavior, not internals. Mocking fetch, async `findBy*`, a11y checks.
* **CSS & styling**

  * CSS Modules/Tailwind vs CSS-in-JS tradeoffs; avoiding specificity wars; theming strategy.
* **TypeScript**

  * Props types vs zod runtime validation, discriminated unions, narrowing.
* **Security**

  * XSS in React (dangerouslySetInnerHTML), escaping, CSP, dependency risk.

**45–55 min — Your questions for them (you evaluate)**
Pick 6–8 from the bank below.

**55–60 min — Wrap-up**

* Summarize what you built, tradeoffs, and what you’d do next with more time.
* Confirm next steps.

---

## Mini Prompt Bank (if they ask you to code)

Use these to clarify before you start:

* “What user behaviors matter most? (keyboard, mobile, screen readers)”
* “Any preferred state library or just React state?”
* “Do we optimize for SSR/streaming or client-only?”
* “OK to stub API with a mock? Any error states to cover?”
* “Should I prioritize tests or features if time runs short?”

---

## React & Best-Practice Questions (for you to ask them)

### Product & UX

* How do you validate frontend requirements—design handoff, edge cases, empty/error/loading states?
* What a11y bar do you hold yourselves to (keyboard parity, screen-reader audits, automated checks)?
* How do you gather real-world performance feedback (Core Web Vitals, RUM)?

### Codebase & Architecture

* What’s your current React architecture (RSC/Next.js, routing, data layer)? Any planned migrations?
* How do you organize components (feature folders, shared UI, design system)? How do you prevent prop drilling hell?
* Where do you draw the line between server and client components? Any caching strategy (React Cache/React Query)?

### Data & State

* Which data-fetching approach is standard (fetch in RSC, React Query, tRPC)? Cache invalidation rules?
* When do you use global state (Redux/Zustand/Context) vs. server cache vs. local state?

### Performance & Quality

* What common render/perf issues you’ve faced? How do you detect re-render thrash in practice?
* Build size & code-splitting strategy? Any guardrails (lint rules, bundle analyzer in CI)?
* Testing pyramid: unit (RTL), component/contract, e2e (Playwright/Cypress). What must be tested before merging?

### Accessibility & UI System

* Do you have a component library/design tokens? How are a11y patterns (dialog, combobox) implemented and tested?
* How do you handle focus management across modals/portals and route transitions?

### DevEx & Process

* Local dev speed (Vite/Turbopack), hot reload reliability, CI times, preview environments?
* Code review norms: what constitutes a “good” PR here? Typical size, expectations, and SLAs?
* Release strategy: feature flags, canary, monitoring, rollback plan?

### Security & Reliability

* How do you prevent client-side XSS and supply-chain risks? Do you use CSP, SRI, Dependabot?
* Error handling: global error boundaries, logging, user-visible fallback patterns?

### Team Growth

* What skills would make someone succeed here in 6–12 months? Any mentorship or tech talks?

---

## Lightning Knowledge Checks (sample questions you might be asked)

* **Why can index keys break list updates?**
  Because insertion/reordering with index keys causes React to reuse DOM nodes incorrectly, leading to state mismatch and janky UI.

* **When pick `useReducer` over `useState`?**
  Complex, multi-field state with tightly coupled transitions; you gain explicit actions and reducer testability.

* **How to prevent stale closures in effects?**
  Depend on stable values (memoized callbacks), move logic inside effect with correct deps, or use an event ref pattern.

* **What causes unnecessary re-renders and how to mitigate?**
  Changing prop/callback identities, broad context providers, derived state. Use memoization, context segmentation, selectors.

* **Accessible modal essentials?**
  ARIA roles, trap focus, restore focus on close, hide background to screen readers, close on Escape, label via `aria-labelledby`.

* **Data fetching without memory leaks?**
  AbortController on fetch, guard setState on unmounted, or delegate to React Query which handles cancellation/staleness.

---

## Tiny Checklist (have this “on the whiteboard”)

* Clarify scope → outline approach → implement MVP UI → wire state → a11y & errors → perf pass → tests (happy path + a11y) → summarize tradeoffs.

If you want, I can spin this into a one-page printable “interview cheat sheet” with a condensed question bank and quick answers.
