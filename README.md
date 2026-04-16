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
│   └── lesson-plan.astro      # Lesson plan viewer page
└── styles/
    └── global.css     # Base reset and diorama canvas geometry
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

### Mobile Resume Viewer (04/15/2026)

- **Resume viewer content** — replaced placeholder with `Resume_doc.png`; desktop keeps scrollable fixed-width viewer, mobile uses letter-size aspect ratio (`8.5:11`) with no padding/scroll.
- **Morph animation** — on portrait devices the resume button (via `style.setProperty`) and PDF container (via `@keyframes mobilePdfOpen/Close`) share the same trajectory and cross-fade, creating a "button morphs into document" effect.
- **Orientation-based layout** — switched mobile breakpoint from `max-width: 768px` to `orientation: portrait` so any device held vertically (including iPads) gets the mobile layout.
- **Z-index layering** — PDF viewer is `z-index: 50` on mobile (above button) and `z-index: 9` on desktop (behind button).
- **Blink fix** — PDF container pre-positioned at animation start state in CSS (without `!important`) and `transition: none !important` applied to prevent `.transition-anim` from racing the keyframe on real devices.
- **Person graphic** — fade curve synced with other interactive buttons (`transform 0.3s ease-out, opacity 0.8s cubic-bezier`); desktop repositioning isolated to `orientation: landscape`.
- **Recommendations page** — added 3D-stacked image carousel, professional/student toggle, and magnifier panel.
