# Funmilayo Oba — Developer Portfolio

🌐 **Live Site:** https://funmioba.vercel.app
📁 **Repository:** https://github.com/Funmi-Oba/my-portfolio

---

## 👩‍💻 About

A highly interactive, visually impressive developer portfolio built with SvelteKit. Designed to feel like an immersive experience — not just a static page. Features a Three.js 3D hero background, a fake VS Code IDE, smooth GSAP animations, and a fully responsive layout.

---

## 🚀 Tech Stack

| Tool | Purpose |
|---|---|
| SvelteKit | Frontend framework |
| TailwindCSS | Utility-first styling |
| Three.js | 3D hero background & particles |
| GSAP + ScrollTrigger | Scroll animations & transitions |
| Monaco-style IDE | Fake VS Code experience |
| Vercel | Deployment & hosting |

---

## 🎯 Features

- ⚡ **Hero Section** — Three.js 3D particle system with rotating wireframe shapes that react to mouse movement
- 🗂️ **Projects Showcase** — 6 real projects displayed in a 3-column grid with browser mockup frames, screenshots, filter tabs, and live/GitHub links
- 📊 **Skills Section** — Animated progress bars across 4 skill categories, triggered on scroll
- 💻 **Fake IDE** — VS Code-inspired code editor with file explorer, syntax highlighting, line numbers, and clickable files that reveal information about me
- 📬 **Contact Section** — Contact form with validation, success state, and social links
- 🌙 **Dark/Light Mode** — Theme toggle with localStorage persistence
- 📱 **Fully Responsive** — Works beautifully on desktop, tablet, and mobile

---

## 🏗️ Project Structure

```
src/
├── routes/
│   ├── +page.svelte        ← Homepage (assembles all sections)
│   ├── +layout.svelte      ← App shell with Navbar
│   └── layout.css          ← Global styles + Tailwind imports
├── lib/
│   └── components/
│       ├── Navbar.svelte   ← Fixed navbar with theme toggle
│       ├── Hero.svelte     ← Three.js 3D section
│       ├── Projects.svelte ← Projects grid with mockups
│       ├── Skills.svelte   ← Animated skill bars
│       ├── IDE.svelte      ← Fake VS Code editor
│       └── Contact.svelte  ← Contact form + socials
static/
└── images/
    └── projects/           ← Project screenshots
```

---

## ⚙️ Setup Instructions

### Prerequisites
- Node.js v18+
- npm

### Installation

```bash
# Clone the repository
git clone https://github.com/Funmi-Oba/my-portfolio.git

# Navigate into the project
cd my-portfolio

# Install dependencies
npm install

# Start development server
npm run dev
```

Open your browser at `http://localhost:5173`

### Build for Production

```bash
npm run build
npm run preview
```

---

## 🎨 Animation Decisions

### Three.js Hero
- 1500 floating particles rotate slowly to create depth
- 4 wireframe geometric shapes (Torus, Octahedron, Tetrahedron, Icosahedron) rotate independently
- Camera position shifts subtly on mouse move using GSAP for a parallax feel
- `alpha: true` on the renderer keeps the background transparent so the dark page shows through

### GSAP ScrollTrigger
- All sections animate in on scroll using `opacity: 0 → 1` and `y: 60 → 0`
- `stagger` is used on project cards and skill categories to create a cascading effect
- `clearProps: 'all'` is applied after animations to prevent lingering inline styles
- `once: true` on skill bars ensures they only animate on first scroll into view

### Skill Bars
- Start at `width: 0%` and animate to the defined percentage
- Uses `ease: 'power2.out'` for a natural deceleration feel

---

## ⚡ Performance Optimization

- **SvelteKit** compiles to vanilla JS with no runtime overhead
- **Lazy rendering** — Three.js only initializes when the Hero component mounts
- **ScrollTrigger** animations are lightweight and GPU-accelerated
- **Images** are served as static assets from the `/static` folder
- **No unnecessary re-renders** — Svelte 5 runes (`$state`, `$derived`) ensure precise reactivity
- **Vercel CDN** serves assets from edge locations globally

---

## ♿ Accessibility Considerations

- Semantic HTML throughout (`nav`, `section`, `main`, `h1-h3`)
- All form inputs have associated `label` elements with matching `for` and `id`
- All interactive elements have `aria-label` attributes
- Keyboard navigable — all links and buttons are focusable
- Color contrast maintained between text and backgrounds
- `animate-pulse` used sparingly and only for decorative indicators
- Theme toggle persists preference via `localStorage`

---

## 🔄 Trade-offs Made

| Decision | Reason |
|---|---|
| No TypeScript | Prioritized speed of development given the deadline |
| Simulated contact form | No backend — form simulates sending with a timeout. Can be replaced with EmailJS or Formspree |
| Static project images | Screenshots served as static files instead of fetched remotely for reliability |
| CSS custom properties over Tailwind theme | More flexibility for dynamic theming with JS |
| Svelte 5 runes over Svelte 4 syntax | Project was scaffolded with Svelte 5 — used modern `$state` and `$derived` throughout |

---

## 📬 Contact

- **Email:** funmilayooba@gmail.com
- **GitHub:** [github.com/Funmi-Oba](https://github.com/Funmi-Oba)
- **LinkedIn:** [linkedin.com/in/funmilayo-oba](https://linkedin.com/in/funmilayo-oba)
- **Portfolio:** [funmilayooba.vercel.app](https://funmilayooba.vercel.app)

---

© 2025 Funmilayo Oba. Built with ❤️ using SvelteKit & TailwindCSS.