# Spice Of Life Media — Website

Premium digital media and creative production studio website for [spiceoflifemedia.com.au](https://www.spiceoflifemedia.com.au).

**Stack:** React 19 · Vite · Tailwind CSS v4 · TypeScript · Wouter · Framer Motion · shadcn/ui (Radix)

---

## Getting started

```bash
npm install        # or: pnpm install
npm run dev        # starts dev server at http://localhost:5173
```

## Scripts

| Command | Description |
|---------|-------------|
| `npm run dev` | Start development server |
| `npm run build` | Production build → `dist/` |
| `npm run preview` | Preview the production build locally |
| `npm run typecheck` | Type-check without emitting |

## Environment variables

Copy `.env.example` to `.env` and adjust:

```bash
cp .env.example .env
```

| Variable | Default | Description |
|----------|---------|-------------|
| `PORT` | `5173` | Dev server port |
| `VITE_API_URL` | `http://localhost:3001` | Backend API URL for contact form proxy |

## Contact form

The contact form (`/src/components/sections/Contact.tsx`) posts to `/api/sol-leads`.

In development this is proxied to `VITE_API_URL` (see `vite.config.ts`).

For production deployment you have two options:
1. **With backend** — deploy the API server and set `VITE_API_URL` in your hosting provider's env config.
2. **Without backend** — replace the `fetch('/api/sol-leads', ...)` call with a third-party form service (Formspree, Netlify Forms, etc.).

## Deployment

The `dist/` folder produced by `npm run build` is a static SPA — deploy to **Vercel**, **Netlify**, **Cloudflare Pages**, or any static host.

### Vercel (recommended)

```
Build command:  npm run build
Output dir:     dist
Install cmd:    npm install
```

### Netlify

Add a `netlify.toml`:

```toml
[build]
  command   = "npm run build"
  publish   = "dist"

[[redirects]]
  from   = "/*"
  to     = "/index.html"
  status = 200
```

## Project structure

```
src/
  assets/          # Images and brand assets
  components/
    layout/        # Navbar, Footer, Layout wrapper
    sections/      # Hero, Services, SelectedWork, Reviews, Contact
    ui/            # shadcn/ui primitives (Radix-based)
  hooks/           # use-toast, use-mobile
  lib/             # utils (cn helper)
  pages/           # Home, not-found
  App.tsx
  main.tsx
  index.css        # Tailwind + CSS variables (brand palette)
public/
  favicon.png
  opengraph.jpg
  robots.txt
  sitemap.xml
index.html
```
