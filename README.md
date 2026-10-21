# Maarif Lesson Planner (version 2.0)

Curriculum-constrained lesson plan generator for English language teachers implementing the Century of Türkiye Education Model (Türkiye Yüzyılı Maarif Modeli), Grades 9–12.

Online Resource 1 for: *Algorithmic Scaffolding for Curricular Fidelity: A Conceptual Analysis of a Generative AI Lesson Planning Tool Aligned with the Century of Türkiye Education Model* (SN Social Sciences).

## Structure

| Path | Content |
|---|---|
| `public/index.html` | Single-page interface (React via CDN). Contains the curricular data structures `TOPICS_BY_GRADE`, `GRAMMAR_BY_GRADE`, `MAARIF_OUTCOMES` and `DROPDOWN_OPTIONS`. |
| `netlify/functions/generate/generate.mjs` | Serverless function. Validates the selections, builds the prompts (`SYSTEM_PROMPT`, `buildUserPrompt`) and streams the lesson plan from Gemini. |
| `netlify.toml`, `package.json` | Deployment configuration. No npm dependencies. |

## Model

Google Gemini 2.5 Flash (`gemini-2.5-flash`) through the Gemini API (`streamGenerateContent`), temperature 0.7. Version 1.x called the preview model `gemini-2.5-flash-preview-09-2025` directly from the browser with the API key in the client code; version 2.0 moved the key and the prompts to the server.

## Running it

Set the environment variable `GEMINI_API_KEY` in the hosting environment (never in the source code), then deploy the folder to Netlify (for local testing: `npx netlify-cli dev`).

The interface is also published to GitHub Pages by `.github/workflows/pages.yml` (Settings > Pages > Source: GitHub Actions). The Pages copy sends requests to the Netlify function, which accepts cross-origin requests only from the GitHub Pages and Netlify origins.

- Netlify: https://maariflessonplanner.netlify.app/
- GitHub Pages: https://murat4595-code.github.io/maariflessonplanner/

No personal or student data are requested or stored.
