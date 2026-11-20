# Hello Pages

A **React** application (TypeScript, Vite) that is automatically built and deployed to **GitHub Pages**.

**Live site:** [https://tegor1212.github.io/hello-pages/](https://tegor1212.github.io/hello-pages/)

---

## Build Locally

```bash
npm install
npm run build
```

The production output is placed in the `dist/` directory.

### Other commands

| Command | Description |
|---|---|
| `npm run dev` | Start the Vite dev server |
| `npm run preview` | Preview the production build locally |
| `npm run lint` | Run ESLint |
| `npm run type-check` | Run TypeScript type checking |
| `npm test -- --run` | Run tests with Vitest |

---

## CI/CD Pipeline

On every push to the `main` branch (and pull requests), the workflow in `.github/workflows/ci-cd.yml` runs:

1. **CI job** (`ubuntu-latest`):
   - Checkout code & setup Node.js 20
   - `npm ci` — install dependencies
   - `npm run lint` — ESLint check
   - `npm run type-check` — TypeScript types
   - `npm test -- --run` — Vitest tests
   - `npm run build` — production build
   - Upload the `dist/` folder as a GitHub Pages artifact

2. **Deploy job** (only on `main` branch, after CI passes):
   - Deploys the artifact to **GitHub Pages** using `actions/deploy-pages@v4`

The live site is updated automatically after every successful run on `main`.