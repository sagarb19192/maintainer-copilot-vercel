# OpenSource Maintainer Copilot — Vercel Edition

A deployable early-stage GitHub issue triage tool with a static HTML/CSS/JavaScript frontend and a Python API running as a Vercel Function. No Streamlit server required.

## Features

- Fetch a public GitHub issue by URL
- Suggest summary, category, priority, missing information and draft reply
- Claude API analysis when configured; clearly labeled heuristic demo mode otherwise
- Editable reply and JSON report download
- Read-only GitHub integration; never posts comments or edits labels

## Deploy to Vercel

1. Create a **public or private GitHub repository** and upload the contents of this folder to the repository root. Do not upload the ZIP itself.
2. In [Vercel](https://vercel.com/new), select **Add New → Project** and import your GitHub repository.
3. Keep **Root Directory** at the repository root. Select **Other** for Framework Preset if prompted. No frontend build command is required.
4. In **Environment Variables**, optionally set `ANTHROPIC_API_KEY` to your own key and `ANTHROPIC_MODEL` to a model available in your account. Without a key, demo mode works without API charges.
5. Click **Deploy**. Open the deployment URL and test the form. `/api/health` reports whether the API is in demo or Claude mode.
6. If you add or change environment variables later, redeploy the project.

**Note:** Live API calls may incur Anthropic charges. Serverless functions have runtime limits; model responses that take too long may fail. Check your Vercel plan's limits.

## Project layout

- `public/index.html` — responsive landing page and application interface
- `api/index.py` — Python HTTP API and GitHub issue loader
- `vercel.json` — route rewrites and function duration
- `requirements.txt` — Python dependencies
- `.env.example` — optional environment variable names

## API

- `GET /api/health` — status and active mode
- `GET /api/issue?url=https://github.com/owner/repo/issues/123` — fetch public issue
- `POST /api/analyze` — JSON `{ "title": "...", "body": "..." }`

## Privacy and security

- Never put API keys in the frontend or commit `.env`.
- Do not submit private security reports, secrets, or confidential data.
- Issue content is sent to Anthropic only in Claude API mode.
- The application does not save issues to a database.
- This is an MVP, **not a production-hardened public API**. Before wider public use, add authentication, rate limits, abuse prevention, monitoring, and a privacy policy.
- GitHub API calls are read-only and limited to public issues.

## Development status

This is a working starter implementation intended for testing and further development, not a claim of a mature startup or guaranteed eligibility for any credit program. Verify the deployed application and current Anthropic model access yourself.

## Roadmap

- [ ] Repository-specific triage policies
- [ ] Evaluation suite for accuracy and draft quality
- [ ] Authentication and rate limits
- [ ] Optional GitHub App integration with review-before-posting
- [ ] Automated integration tests and monitoring

## License

MIT.
