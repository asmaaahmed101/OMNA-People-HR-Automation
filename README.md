# OMNA People — HR Automation with n8n

A small HR system that answers policy questions in a chat, screens job applications with AI, and sends interview coaching reports. Everything runs on n8n workflows behind a single-page website.

**Live site:** https://asmaaahmed101.github.io/OMNA-People-HR-Automation/

## Workflows

| File | Trigger | What it does |
|---|---|---|
| recruitment-1-intake.json | Form Trigger | Collects the applicant's details and CV through a public form. |
| recruitment-2-scan.json | Webhook (from Intake) | An AI agent reads the application, scores the fit and writes the result to a tracking sheet. |
| recruitment-3-handler.json | Error Trigger | Catches errors from every workflow and logs them in one place. |
| hr-policy-chatbot.json | Chat Trigger | An AI agent answers HR questions from the company policy documents (vector store) and names the policy it used. |
| job-application-coach.json | Form Trigger | Takes a CV and returns an interview coaching report. |

## Services needed

- n8n (self-hosted in Docker)
- Groq API key (chat models)
- Google Gemini API key (embeddings)
- Google Sheets (application tracking)
- ngrok (public URL for the local n8n)

## How to import

1. In n8n, open the Workflows list and choose **Import from file** for each `.json` file.
2. Add your own credentials where a node asks for them (Groq, Gemini, Google Sheets) and fill in the blank document and sheet IDs.
3. Load your policy documents through the Policy Loader branch of the HR Policy Chatbot, then publish every workflow.
4. To point the website at your own server, edit the `CONFIG` block at the bottom of `index.html` with your n8n base URL and trigger paths.

## Notes

- The site keeps the `ngrok-skip-browser-warning` header on chat requests so free ngrok does not intercept them.
- All visitor and AI text is inserted with `textContent`, never `innerHTML`.
- No keys, emails or private IDs are stored in this repository.
