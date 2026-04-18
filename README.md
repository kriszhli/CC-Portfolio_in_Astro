# Interactive Portfolio Website for Ms. Cici Qiao

A simple interactive portfolio landing page built with [Astro](https://astro.build). The site features a number of physics-based interactions without any runtime UI frameworks.

**Live site:** [kriszhli.github.io/CC-Portfolio_in_Astro](https://kriszhli.github.io/CC-Portfolio_in_Astro)


## Tech Stack

| Layer | Technology |
|---|---|
| Framework | Astro 5 (static output) |
| Styling | Vanilla CSS with custom properties |
| Scripting | Vanilla JavaScript (no runtime framework) |
| Images | Astro `<Image />` component (automated optimization) |
| Deployment | GitHub Actions → GitHub Pages |

## Project Structure

```
src/
├── assets/
│   └── PNGs/          # Artwork (made by Seedream) processed at build time by Astro
├── components/
│   └── InteractiveElement.astro   # Reusable interactive icon with physics props
├── pages/
│   ├── index.astro            # Landing page — layout, CSS, and interaction logic
│   ├── recommendations.astro  # 3D carousel + magnifier for recommendation letters
│   └── lesson-plan.astro      # Interactive binder UI with PDF.js-powered lesson viewer
public/
└── assets/
    └── PDFs/          # Lesson plan PDFs (SmartCookie, Math, SocialStudies) — served with stable URLs
src/styles/
└── global.css         # Base reset and diorama canvas geometry
```

---

## Deployment

The site is built and deployed automatically via GitHub Actions on every push to `main`. The workflow runs `npm install && npm run build`, uploads the `./dist` directory as a Pages artifact, and deploys it.

```yaml
- run: npm install
- run: npm run build
- uses: actions/upload-pages-artifact@v3
  with:
    path: ./dist
```

GitHub Pages is configured to deploy from the Actions source in the repository settings.

---

## Changelog

### Mobile Resume Viewer & Recommendations Page (04/15/2026)

- **Mobile resume viewer** — portrait devices get a morph animation where the resume button transitions into a letter-size (8.5:11) document; orientation-based breakpoint ensures iPads are covered.
- **Resume rendering fixes** — z-index layering, blink prevention, and person graphic sync resolved cross-device glitches on the desktop/mobile split layout.
- **Recommendations page** — 3D-stacked image carousel with a professional/student toggle and a magnifier panel for viewing recommendation letters.

### Lesson Plan Binder (04/16/2026)

- **Binder UI** — lesson-plan page styled as an interactive physical binder (spine, ring holes, and side tabs) to reinforce a school-supply theme.
- **Glass & lighting** — unified glassmorphism system across spine and tabs; reactive light blooms and spine tint shift color (pink → green → blue) based on the active lesson.
- **PDF.js pipeline** — custom canvas renderer replaces `<iframe>` embeds; pages scale to fit width at `devicePixelRatio` resolution with lazy loading per tab and debounced resize re-rendering.
- **Animations** — 3D `rotateY` page-turn on tab switch; smooth tab slide, color, and bloom transitions throughout.

### Lesson Plan & Recommendations Refinements (04/17/2026)

- **Binder page-flip fix** — corrected the 3D `rotateY` page-turn animation sequencing so pages always complete their exit before the next page enters.
- **Tab scroll reset** — switching binder tabs now scrolls the PDF viewer back to the top of the document.
- **Lesson-plan → home transition** — added a white-fade-out on the back button click to match the rest of the site's navigation feel; removed legacy custom cursor code.
- **Mobile resume viewport** — resolved remaining glitch where the PDF container could overflow the screen; CSS cascade order fixed so portrait-specific overrides reliably win over shared styles; `global.css` viewport geometry tightened.
- **Recommendations magnifier** — desktop view now has a drag-to-pan magnifying viewport that renders a zoomed-in region of the currently selected letter; hover to reveal, drag to move the focus point.
