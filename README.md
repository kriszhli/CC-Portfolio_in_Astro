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
│   ├── PNGs/          # Artwork (made by Seedream) processed at build time by Astro
│   └── resume.png
├── components/
│   └── InteractiveElement.astro   # Reusable interactive icon with physics props
├── pages/
│   └── index.astro    # Landing page — layout, CSS, and interaction logic
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
