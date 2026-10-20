# Live Hiring Assistant (Recruitment Co-pilot)

> **From the What I Built (WIB) podcast, Episode 01 (Agent 03).** A Podcast for AI Builders.

A co-pilot that sits alongside a live interview: it keeps the transcript, suggests
the next question, and drafts a structured, evidence-backed feedback report for the
hiring panel. It turns about an hour of post-interview write-up into about 10 minutes.
The human makes the hiring decision; the co-pilot does the paperwork.

**Try it:** https://luna-interview-copilot.vercel.app (opens with a synthetic demo interview)

## Input

- **Job description**, **candidate CV** and an optional **rubric** (paste or upload .txt / .md)
- **Interview transcript**: paste or upload one, type live notes line by line, or turn on the browser's live mic transcription
- **Your own AI key**: Anthropic (default `claude-haiku-4-5`) or OpenAI (default `gpt-4o-mini`)

## Process

1. **Prepare**: load the JD, CV and rubric. One criterion per line; add `| score` for a 1–5 rating and `| guidance` to tell the AI what good looks like. The default rubric is role alignment, product judgment, analytical depth, execution, communication, strengths and an open question for the next round.
2. **Live interview**: start the timer, add notes or let the mic transcribe. Hit **Suggest follow-up** for a next question aimed at criteria not covered yet.
3. **Draft**: **Finish & draft report** sends the transcript, JD and rubric to your model. It scores every criterion with a quoted line of evidence, judges the whole interview rather than the last 10 minutes (no recency bias), marks anything not discussed as "Not covered" instead of guessing, and ignores protected characteristics.
4. **Review**: every field stays editable; your edits are never overwritten. Change the recommendation if you disagree.

## Output

- **Panel recommendation**: Strong Hire / Hire / Lean No Hire / No Hire with rationale and next step
- **Scorecard**: score plus evidence quote per rubric criterion, strengths, areas to validate
- **Exports**: Slack-ready text, Markdown download, and JSON with a flat `portal_fields` map for HR portals and forms (Keka, Workday, Greenhouse, Google Forms, Microsoft Forms)

## Setup

It's a single static file, `app/index.html`. No build step, no backend, no database.

- **Run locally**: `cd app && python3 -m http.server 8000`, then open http://localhost:8000.
  (Opening the file directly works too, but the live mic needs `localhost` or `https`.)
- **Deploy your own** (free): `npx vercel deploy app --prod`, or drag the `app` folder into Netlify / GitHub Pages.
- **Add a key**: click **✦ Add AI key** in the app, choose a provider, paste your key.

## Privacy

- Your API key is stored only in your browser's localStorage and is sent only to the provider you chose. **Clear key** removes it.
- Interview data stays in the tab (sessionStorage) and is gone when you close it. Nothing is stored on a server.
- Chrome's live mic sends audio to Google's speech service. Use pasted transcripts if that's not OK.
- The demo candidate, interviewers and portals are fictional.

## How I use it at work

In my own setup the transcript comes from my meeting-notes tool and the feedback goes
straight into the HR portal's form through its API. This public version swaps those
for paste / upload and portal-ready exports, so it works for anyone with no accounts.
