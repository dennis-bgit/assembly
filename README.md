# SOW Builder

One web app for Sourcepass MCOE statements of work. The sales team signs in with their Sourcepass account, picks a SOW type (Microsoft Intune or Migrations today), builds the SOW from the calculator, saves drafts the whole team can open, and exports a real text PDF.

It runs as one Azure Container App. Bicep describes every resource, and GitHub Actions deploys each change with no secrets stored in GitHub.

| Folder | What's in it |
| --- | --- |
| `app/server/` | Node.js 24 + TypeScript: sign-in, the API, storage, and server PDF rendering (Playwright) |
| `app/web/` | The home page, the design system assets, and the builders (`sow-types/<type>/builder.html`, as published from Claude) |
| `infra/` | Bicep for every Azure resource; `main.bicepparam` holds the live values |
| `library/` | SOW text per type (filled in Phase 5) |
| `.github/workflows/` | `infra.yml` (what-if on pull requests, deploy on main) and `app.yml` (test, build, deploy, library sync) |
| `docs/` | The plan, the setup guide, the handoff notes, and the request for IT |

## Run it locally

```bash
cd app
npm install
npx playwright-core install chromium   # once, for server PDFs
npm run dev                            # http://localhost:8080
```
