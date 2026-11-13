---
name: site-animations
description: Add GSAP animations, Lenis smooth scroll and React Bits components to a website project. Use when the user wants to animate a site, add smooth scrolling, scroll-triggered animations, or React Bits components.
metadata:
  origin: thomaslachaud1704-art
  verified: 2026-11-13
---

# Site Animations (GSAP + Lenis + React Bits)

Sources (official repositories, checked 2026-11-13):

- GSAP skills: <https://github.com/greensock/gsap-skills> (MIT) — install the `gsap-skills@ecc` plugin for detailed GSAP guidance
- Lenis: <https://github.com/darkroomengineering/lenis> (npm `lenis` 1.3.27, MIT)
- React Bits: <https://github.com/DavidHDev/react-bits> (MIT + Commons Clause)

## When to Use

- The user wants animations, scroll effects or smooth scrolling on a website
- The user mentions GSAP, ScrollTrigger, Lenis or React Bits

## How It Works

Ask for the user's approval before installing packages or editing files. Work on a new git branch.

### 1. Analyze the project

Detect and summarize: framework (React/Next.js, Vue/Nuxt, Astro, Svelte, static HTML), package manager (npm/pnpm/yarn/bun via lockfile), TypeScript, Tailwind, shadcn (`components.json`). Use the detected package manager for every install below.

### 2. GSAP

- `npm install gsap`
- React projects: also `npm install @gsap/react` and use the `useGSAP()` hook instead of `useEffect` (automatic cleanup).
- Register plugins once: `gsap.registerPlugin(ScrollTrigger)` (and `useGSAP` in React).
- Follow the `gsap-skills` plugin skills (gsap-core, gsap-scrolltrigger, gsap-react, gsap-performance).

### 3. Lenis (smooth scroll)

- `npm install lenis` and import `lenis/dist/lenis.css`.
- Vanilla / non-React — sync with ScrollTrigger (from the Lenis README):

```js
const lenis = new Lenis();
lenis.on('scroll', ScrollTrigger.update);
gsap.ticker.add((time) => { lenis.raf(time * 1000); });
gsap.ticker.lagSmoothing(0);
```

- React — use `lenis/react` at the app root (from the lenis/react README):

```jsx
import gsap from 'gsap'
import { ReactLenis } from 'lenis/react'
import { useEffect, useRef } from 'react'

function App() {
  const lenisRef = useRef()
  useEffect(() => {
    function update(time) { lenisRef.current?.lenis?.raf(time * 1000) }
    gsap.ticker.add(update)
    return () => gsap.ticker.remove(update)
  }, [])
  return <ReactLenis root options={{ autoRaf: false }} ref={lenisRef} />
}
```

- Vue/Nuxt: Lenis ships a `vue` package — read its README in the Lenis repo before using it.
- Respect `prefers-reduced-motion`: disable smooth scroll and heavy animations when it is set.

### 4. React Bits (React projects only)

- Not React → skip and tell the user.
- If shadcn is not initialized, propose `npx shadcn@latest init` first.
- Add components with `npx shadcn@latest add @react-bits/<Name>-<TS|JS>-<TW|CSS>` (TS/JS per project, TW if Tailwind else CSS). Alternative: `npx jsrepo@latest add https://reactbits.dev/r/<Name>-<TS|JS>-<TW|CSS>`.
- Propose 3–5 components that fit the site before adding any; component names are listed on <https://reactbits.dev>.
- License is MIT + Commons Clause: remind the user to read the repository LICENSE if the site is sold or delivered to a client.

### 5. Verify

Run the build and the dev server, fix errors, check the page in a browser if available, then commit on the branch. Do not push without the user's approval.

## Examples

- "Ajoute un scroll fluide et des animations au scroll sur mon site" → steps 1–3, then 5
- "Ajoute un texte animé React Bits sur la home" → steps 1, 4, 5
