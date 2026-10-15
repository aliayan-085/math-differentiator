# AI Math Differentiator: Quadratic Equations

Web app for the course *Educational Technology & AI* (Topic 8: AI for Differentiated Learning).
One core topic, **quadratic equations**, is adapted into three difficulty levels. An AI model (Google Gemini)
writes the problem text, hints, feedback and explanations for the chosen level.

**Live demo:** _paste your Vercel link here_

## Levels

| Level | Task | AI support |
|-------|------|-----------|
| 1 Foundation | `x² + bx + c = 0`, small integer roots | Simple language, numbered steps, direct hints |
| 2 Standard | `ax² + bx + c = 0`, integer roots | Concise hints that name the method |
| 3 Advanced | Real-world word problem (garden area) | Guiding questions, check the result against reality |

## How it works

1. `index.html` generates the numbers and the **correct answers with plain JavaScript** (the AI never does the math).
2. The page sends the task facts and the level to `/api/generate`.
3. `api/generate.js` (a Vercel serverless function) adds the level's system prompt and calls the Gemini API.
   The API key is stored as a server environment variable, so it is never exposed in the browser.
4. The answer is checked by code. For Level 3 the page also verifies that the AI text contains the right numbers
   and uses a template if it does not.

## Project structure

```
index.html        user interface + math generation and answer checking
api/generate.js   server function: system prompts + Gemini API call
README.md
```

## Run / deploy

1. Get a free API key at <https://aistudio.google.com/apikey>.
2. Push this repository to GitHub and import it in Vercel.
3. In Vercel, Project Settings → Environment Variables, add `GEMINI_API_KEY` (your key).
   Optional: `GEMINI_MODEL` (default `gemini-3.6-flash`; use `gemini-2.5-flash` if the default is unavailable).
4. Deploy (or redeploy after adding variables).

Local test: `npm i -g vercel`, then `vercel dev` in this folder (with the same environment variables).

## Notes

- Never commit the API key to the repository.
- Prompts are in `api/generate.js` (`PROMPTS` and `KINDS`).
