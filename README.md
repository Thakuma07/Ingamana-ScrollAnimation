# Ingamana Scroll Animation

A visually immersive **scroll-driven animation** built with **Next.js**, **GSAP**, and **Lenis**. As the user scrolls, rows of project cards dynamically expand in width to create a fluid, cinematic reveal effect — inspired by editorial portfolio layouts.

<img width="1920" height="1080" alt="Screenshot (355)" src="https://github.com/user-attachments/assets/7c15ebf1-3e8e-4fe5-a2f7-a95efa3da169" />

---

## ✨ Features

- **Scroll-driven Width Expansion** — Each row of project cards expands from a compressed state to a full-width view as it enters the viewport.
- **Smooth Scrolling** — Powered by [Lenis](https://lenis.darkroom.engineering/) for buttery, momentum-based scroll behaviour.
- **GSAP Ticker Integration** — Lenis is driven by the GSAP ticker for frame-perfect synchronisation with all animations.
- **Responsive Design** — Automatically adjusts start and end widths for mobile and desktop breakpoints.
- **Resize Handling** — Section height and row widths recalculate correctly on window resize.
- **Dynamic Project Grid** — 10 rows × 9 cards built from a looping project data array, giving an infinite-feeling gallery.
- **Optimised Font** — Uses PP Neue Montreal via CDN for a clean, editorial typographic feel.

---

## 🛠️ Tech Stack

| Technology | Version | Purpose |
|---|---|---|
| [Next.js](https://nextjs.org/) | 16.1.6 | React framework & routing |
| [React](https://react.dev/) | 19.2.3 | UI component layer |
| [GSAP](https://gsap.com/) | ^3.14.2 | Animation ticker & scroll progress |
| [Lenis](https://lenis.darkroom.engineering/) | ^1.3.17 | Smooth scroll engine |
| [PP Neue Montreal](https://pangrampangram.com/) | CDN | Editorial typography |

---

## 📁 Project Structure

```
ingamana-scroll/
├── public/
│   └── images/               # Project card images (img1.jpg – img16.jpg)
├── src/
│   ├── app/
│   │   ├── favicon.ico
│   │   ├── globals.css        # Global reset, typography, layout styles
│   │   ├── layout.js          # Root layout with Geist font & metadata
│   │   ├── page.js            # Home page — Lenis + GSAP setup, renders sections
│   │   └── page.module.css
│   └── components/
│       └── Projects/
│           ├── Projects.jsx   # Main scroll animation component
│           └── projects.js    # Static project data array
├── jsconfig.json
├── next.config.mjs
├── package.json
└── README.md
```

---

## ⚙️ How the Animation Works

### 1. Layout

The page is split into three vertical sections:

- **Intro** — A full-viewport-height placeholder section before the animation.
- **Projects** — The animated grid containing 10 rows of 9 project cards.
- **Outro** — A full-viewport-height placeholder section after the animation.

### 2. Row Width Interpolation

Each row starts at **125% viewport width** (desktop) or **250%** (mobile) — wide enough to overflow the screen. As the user scrolls and a row enters the viewport, its `width` is interpolated towards **500%** (desktop) or **750%** (mobile):

```
width = rowStartWidth + (rowEndWidth - rowStartWidth) * progress
```

`progress` is calculated from each row's position relative to the scroll offset and viewport height, clamped between `0` and `1`.

### 3. GSAP Ticker

The `onScrollUpdate` function is registered with `gsap.ticker.add()` so it runs on every animation frame — keeping the widths in perfect sync with the smooth-scrolled position reported by Lenis.

### 4. Section Height

Because the rows are wider than the viewport, they overflow horizontally (clipped by `overflow: hidden`). The section's explicit height is calculated dynamically as:

```
height = (expandedRowHeight × numRows) + (gap × (numRows - 1)) + (padding × 2)
```

This ensures the scroll distance is long enough for all rows to fully animate in.

---

## 🚀 Getting Started

### Prerequisites

- [Node.js](https://nodejs.org/) v18 or later
- npm / yarn / pnpm / bun

### Installation

Clone the repository and install dependencies:

```bash
git clone https://github.com/your-username/ingamana-scroll.git
cd ingamana-scroll
npm install
```

### Running the Development Server

```bash
npm run dev
# or
yarn dev
# or
pnpm dev
# or
bun dev
```

Open [http://localhost:3000](http://localhost:3000) in your browser to see the animation in action.

### Building for Production

```bash
npm run build
npm run start
```

---

## 🖼️ Project Data

Project cards are defined in `src/components/Projects/projects.js`. Each entry has the following shape:

```js
{ name: "Project Name", year: 2024, img: "/images/imgN.jpg" }
```

The 16 projects in the dataset are cycled across all 90 card slots (10 rows × 9 columns) using a modulo index. To add or change projects, edit the `PROJECTS` array in that file and drop the corresponding images into `public/images/`.

---

## 🎨 Customisation

| What to change | Where |
|---|---|
| Number of rows | `TOTAL_ROWS` constant in `Projects.jsx` |
| Cards per row | `PROJECTS_PER_ROW` constant in `Projects.jsx` |
| Start/end widths | `rowStartWidth` / `rowEndWidth` refs in `Projects.jsx` |
| Mobile breakpoint | `isMobile` check (`window.innerWidth < 1000`) in `Projects.jsx` |
| Global styles | `src/app/globals.css` |
| Project cards & images | `src/components/Projects/projects.js` + `public/images/` |
| Page metadata | `src/app/layout.js` |

---

## 📦 Dependencies

### Production

```json
{
  "gsap": "^3.14.2",
  "lenis": "^1.3.17",
  "next": "16.1.6",
  "react": "19.2.3",
  "react-dom": "19.2.3"
}
```

### Development

```json
{
  "babel-plugin-react-compiler": "1.0.0"
}
```

---

## 🌐 Deployment

The easiest way to deploy this project is via the [Vercel Platform](https://vercel.com/new), which is built by the creators of Next.js.

1. Push your repository to GitHub.
2. Import the project on [vercel.com](https://vercel.com).
3. Vercel will auto-detect Next.js and configure the build for you.

For other platforms, refer to the [Next.js deployment documentation](https://nextjs.org/docs/app/building-your-application/deploying).

---

## 📄 License

This project is open-source and available under the [MIT License](LICENSE).

---

> Built with ❤️ and a love for smooth scrolling.
