# Agent Guide: Estate Portfolio

## Overview
**Estate** is a React portfolio website built with Vite, Tailwind CSS, and animations. It's a single-page application showcasing real estate projects with sections for Header, About, Projects, Testimonials, and Contact.

## Quick Start
- **Dev server**: `npm run dev` (runs Vite on default port, auto-reload on file changes)
- **Build**: `npm run build` (outputs to `dist/`)
- **Lint**: `npm run lint` (checks for ESLint violations)
- **Base path**: `/timate` (configured in vite.config.js — deployment target)

## Project Structure
```
src/
  ├── components/          # Section components (Header, About, Projects, etc.)
  ├── assets/             # Static assets and image imports (assets.js)
  ├── App.jsx             # Root component (orchestrates sections)
  └── main.jsx            # React entry point
```

## Key Patterns & Conventions

### Styling
- **Tailwind CSS** for all styling (no CSS modules or styled-components)
- Responsive classes: `sm:`, `md:`, `lg:` for mobile-first design
- Custom Tailwind config in `tailwind.config.js` (currently minimal, extending defaults)
- Inline styles used only for dynamic values (e.g., `backgroundImage`)

### Animations
- **motion/react** library (formerly Framer Motion v7) for animations
- Common pattern: `whileInView` with `initial` and `transition` props
- Animations trigger when sections scroll into view: `viewport={{once:true}}`
- Example: fade-in + slide-up on scroll (Header.jsx:10-14)

### Component Structure
- Functional components only (no class components)
- Components wrapped with `motion.div` for scroll-triggered animations
- Responsive container pattern: `container mx-auto py-4 px-6 md:px-20 lg:px-32`
- Section IDs for anchor navigation (e.g., `id='Header'`, `id='Projects'`)

### Assets
- Image imports centralized in `src/assets/assets.js`
- Reference assets as `assets.header_img`, `assets.project_name`, etc.
- Keep assets.js up-to-date when adding new images

### React Toast Notifications
- `react-toastify` for alerts/notifications
- `ToastContainer` mounted in App.jsx
- Import and use: `import { toast } from 'react-toastify'; toast.success("Message")`

## Development Workflow
1. Start dev server: `npm run dev`
2. Edit components in `src/components/`
3. Update Tailwind classes for styling
4. Use `motion` props for scroll animations
5. Add images to assets and reference via `assets.js`
6. Run `npm run lint` before committing

## Common Tasks

**Add a new section**: Create component in `src/components/`, add to App.jsx, apply motion animations, add section ID for navigation.

**Update styling**: Use Tailwind classes directly in JSX. Adjust responsive prefixes (`sm:`, `md:`, `lg:`) for mobile-friendly layouts.

**Fix animations**: Check motion props (`initial`, `whileInView`, `transition`). Adjust timing in `transition={{duration: X}}` or scroll trigger in `viewport`.

**Add new image**: Place in `public/` or import in `assets.js`, then reference as `assets.image_name`.

## Notes
- No TypeScript or prop validation (consider adding PropTypes if validation becomes necessary)
- ESLint configured with React hooks plugin — follow react-hooks rules
- React 19.2.0 features available (latest React version)
- All CSS is utility-based (Tailwind) — no CSS-in-JS or preprocessors beyond PostCSS
