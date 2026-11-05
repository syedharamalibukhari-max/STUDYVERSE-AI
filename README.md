# StudyVerse AI

A responsive learning-platform starter for computing students in Pakistan. It includes degree and course discovery, curriculum source notes, a sample learning chapter, PDF export, a quiz, a local study planner, a coding editor (no code execution), and **HAM**, the StudyVerse AI study tutor.

## What's included

- React 19 + TypeScript + Vite frontend.
- Responsive home page, degree catalogue and degree detail pages.
- Searchable course library and subject/chapter navigation.
- HEC curriculum source registry with explicit verification labels and source links.
- Sample Data Structures chapter, browser PDF export and print layout.
- Sample interactive quiz.
- Local study checklist saved in the current browser.
- Client-side code editor for C++, Python and JavaScript examples. It does not execute code.
- HAM chat with local conversation history, copy/export, text/Markdown/CSV attachment support and a clearly labelled demo fallback.
- Netlify Function for server-side OpenAI-compatible chat. The API key is never placed in frontend code.
- PostgreSQL schema foundation in `database/schema.sql` for a future authenticated/persistent product.

## Run locally

Requirements: Node.js 20 or newer and npm.

```bash
npm install
npm run dev
```

Open the local URL printed by Vite (normally `http://localhost:5173`).

## Activate live HAM

Without an API key, HAM deliberately stays in demo mode. To enable real AI answers:

1. Create an API key with your chosen AI provider.
2. For local testing with Netlify Functions, install the Netlify CLI and run `netlify dev` after setting `OPENAI_API_KEY` in your local environment. Do not commit a `.env` file.
3. On Netlify, open **Site configuration → Environment variables**.
4. Add `OPENAI_API_KEY` with your private key. Optionally add `OPENAI_MODEL` (default: `gpt-4o-mini`).
5. Trigger a new deploy. The key is read only by the server-side Netlify Function; never use a `VITE_` prefix for secrets.

AI API usage may cost money depending on provider, model and usage. Check provider pricing and set a budget/usage limit. Do not paste private API keys into public repositories or chat messages.

HAM currently accepts text, Markdown and CSV attachments up to 100 KB and includes their text in the next prompt. PDF/DOCX image extraction, long-term account memory, streaming, rate limiting and persistent server-side chat storage are not implemented in this starter.

## Deploy to Netlify (free static hosting tier)

### Method A — GitHub import (recommended)

1. Extract the ZIP file.
2. Open GitHub and create a new repository named `studyverse-ai`.
3. In the repository page choose **Add file → Upload files**. Upload the *contents* of the extracted `studyverse-ai` folder (including `src`, `public`, `netlify`, `package.json`, `netlify.toml`, etc.). Do not upload `node_modules` or `.env`.
4. Commit the files to the `main` branch.
5. Sign in to Netlify and choose **Add new site → Import an existing project**.
6. Connect GitHub and select `studyverse-ai`.
7. Confirm these build settings:
   - Build command: `npm run build`
   - Publish directory: `dist`
   - Functions directory: `netlify/functions` (already set in `netlify.toml`)
8. Choose **Deploy**. Netlify installs dependencies and builds the site.
9. When the deploy succeeds, open the generated `*.netlify.app` URL.
10. To activate live HAM, add `OPENAI_API_KEY` under Site configuration → Environment variables and redeploy.

### Method B — Netlify manual deploy

Manual drag-and-drop deploys only work with a built `dist` folder. On a computer with Node.js 20+:

```bash
npm install
npm run build
```

Then drag the generated `dist` folder to Netlify Drop. This static-only method does not deploy the Netlify Function, so HAM will use demo mode. Use Method A to deploy both the website and HAM function.

## Important current scope

This is a working frontend foundation, not a finished commercial university LMS. The catalogue has curriculum metadata and sample learning content; it does not yet contain complete, verified notes for every subject/chapter. The admin route is deliberately disabled. User sign-in, roles, a connected PostgreSQL database, admin CMS, cross-device progress sync, private document storage, full PDF/DOCX analysis, secure code execution, analytics, production rate limits and a complete legal review still need implementation before offering those features as live services.

The study planner and HAM chat history are stored in the visitor's browser only. Clearing browser data can remove them; they do not sync across devices.

## Curriculum accuracy

The catalogue labels notified HEC frameworks, specialization clusters, university-specific programme titles and recommended/illustrative material separately. Do not present a suggested HEC semester distribution as the mandatory scheme of every university. Students should verify programme requirements with their awarding institution.

Primary references included in the project:

- HEC BS Computer Science curriculum (2025): https://www.hec.gov.pk/english/services/universities/RevisedCurricula/Documents/2025-2026/COMPUTER-SCIENCE.pdf
- HEC BSCS specialization announcement: https://www.hec.gov.pk/english/news/news/Pages/HEC-in-Collaboration-with-Academia.aspx
- HEC BS Cyber Security curriculum (2026): https://www.hec.gov.pk/english/services/universities/RevisedCurricula/Documents/2025-2026/CYBER-SECURITY.pdf
- HEC revised curricula index: https://www.hec.gov.pk/english/services/universities/RevisedCurricula/Pages/default.aspx
- HEC Computing Disciplines curriculum (2023; historical reference): https://www.hec.gov.pk/english/services/universities/RevisedCurricula/Documents/2022-2023/Computing-Disciplines.pdf

## Security checklist before scaling

- Keep all provider secrets in server-side environment variables.
- Add authentication, server-side authorization, database row-level policies and audit logs before enabling student accounts or admin controls.
- Add request quotas and abuse protection to the AI endpoint before public high-traffic use.
- Validate and scan uploaded files; store private uploads outside the public web root.
- Never execute user-submitted code on the application server. Use a properly isolated execution service if a code runner is added.
- Review privacy, terms, cookie/analytics notices and contact details against the actual data practices and applicable law.
