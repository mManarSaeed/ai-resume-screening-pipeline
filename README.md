# AI-Powered Resume Screening Pipeline

An **n8n** workflow that reads a resume and a job description, scores the match out of 100, saves the result and keeps HR informed automatically.

> Personal learning project, built solo during an AI Automation & AI Agents course (Aug 2026).

## What it does

1. A **form** collects the candidate's resume (file) and the job description.
2. Text is extracted from the resume file.
3. **Three LLM chains** (Groq, Llama 3.3 70B) with structured JSON output:
   - extract the candidate profile (name, contact, education, experience, skills),
   - extract the job requirements (required and preferred skills),
   - evaluate the candidate against the job.
4. The score uses a weighted formula:

| Criteria | Weight |
|---|---|
| Skills match | 40% |
| Experience relevance | 25% |
| Education match | 15% |
| Projects relevance | 10% |
| Certifications | 10% |

5. Result levels: **80–100** Strong Match (proceed to interview), **60–79** Potential Match (review manually), **0–59** Weak Match (reject).
6. Everything is saved in Google Sheets (`Candidates Screening`).
7. The candidate receives an automatic feedback email, and HR is alerted by email only when the candidate is a strong match.
8. A scheduled run sends HR a daily report with candidates ranked by score.

## Tech stack

n8n (Form Trigger, Extract From File, Basic LLM Chain, Structured Output Parser), Groq, Google Sheets, Gmail.

## Run it yourself

1. Import `workflow/ai-resume-screening-pipeline.json` into n8n.
2. Add your own credentials for Groq, Google Sheets and Gmail.
3. Create a Google Sheet tab named `Candidates Screening` and set its ID where the nodes show `YOUR_GOOGLE_SHEET_ID`.
4. Replace the HR email placeholder with your own address.
5. Activate the workflow and submit the form.

The export contains no passwords, API keys or tokens.

## What I learned

- Asking an LLM for structured JSON makes its output usable in later steps.
- A clear scoring formula makes the AI decision easier to explain and to check.

## Author

Manar Saeed Ibrahim – [LinkedIn](https://www.linkedin.com/in/manar-s-836718242)
