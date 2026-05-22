# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Commands

- **Dev server**: `npm run dev` (Vite, HMR enabled)
- **Build**: `npm run build` (outputs to `dist/`)
- **Preview build**: `npm run preview`
- **Lint**: `npm run lint` (ESLint with React hooks + refresh plugins)
- **Single file lint**: `npx eslint src/path/to/file.jsx`

## Architecture

**Estate** is a single-page React portfolio for a real estate company. Built with Vite 7 + React 19 + Tailwind CSS 3 + motion (formerly Framer Motion). Deployed at base path `/timate`.

### Component structure

`App.jsx` mounts all sections vertically as a flat list — no router:

1. **Header** → renders `Navbar` + hero with background image and CTA buttons. Navbar includes desktop nav links and a mobile menu with body scroll lock.
2. **About** → brand image + stats grid (years, projects, sq ft delivered) + description.
3. **Projects** → horizontal slider with prev/next buttons. On desktop (>=1024px) shows all cards; on mobile shows one at a time with translateX animation. Data from `projectsData` in assets.js.
4. **Testimonials** → static grid of 3 customer cards with star ratings.
5. **Contact** → form (name, email, message) that submits to web3forms.com API. Uses `VITE_ACCESS_KEY` env var. Shows toast notification on success/error via `react-toastify`.
6. **Footer** → logo + company links + copyright.

### Key patterns

- **All data is hardcoded** in `src/assets/assets.js` — no API calls. Add projects/testimonials by editing that file.
- **Scroll-triggered animations**: every section is wrapped in `<motion.div>` with `initial`, `whileInView`, `viewport={{once:true}}` from the `motion` library.
- **Anchor navigation**: section `id` attributes (e.g., `id="Projects"`) linked via `<a href="#Projects">`. No React Router.
- **Responsive container pattern**: `container mx-auto py-4 px-6 md:px-20 lg:px-32`
- **Toast notifications**: `ToastContainer` is in App.jsx. Import `{ toast }` from `react-toastify` and call `toast.success()` or `toast.error()`.
- **Environment variables**: `VITE_ACCESS_KEY` (Web3Forms API key) in `.env`. See vite.config.js for `VITE_BASE_PATH`.

### Image assets

All images are imported in `src/assets/assets.js` and exported as the `assets` object and data arrays (`projectsData`, `testimonialsData`). Reference as `assets.header_img`, not raw path strings.

### Styling

Tailwind CSS utility classes only. Custom font (Outfit) via Google Fonts in `index.css`. No CSS modules or styled-components. Tailwind config at `tailwind.config.js` — currently minimal with no custom theme extensions.