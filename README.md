# Resume vs Job Match AI

An AI-powered tool that compares a resume with a job description and provides a clear match score, skill overlap, missing requirements, and practical ways to improve the resume.

## Overview

Job seekers often have difficulty understanding how closely their experience aligns with a specific role. Resume vs Job Match AI solves this problem by analyzing the resume and job description together, identifying evidence-based strengths and gaps, and turning the comparison into actionable feedback.

The app is designed to provide a useful starting point for tailoring a resume. It does not make hiring decisions or replace a recruiter’s judgment.

## Tools Used

- **Python Flask** — backend API and request validation
- **Google Gemini API** — AI-powered resume and job description comparison
- **HTML, CSS, and JavaScript** — frontend experience, implemented with React, TypeScript, and Vite
- **Replit Secrets** — secure storage for `GEMINI_API_KEY`

## Features

- Resume and job description text areas
- AI-generated match score from 0 to 100
- Structured JSON output containing:
  - `match_score`
  - `matching_skills`
  - `missing_skills`
  - `improvement_suggestions`
- Clear skill badges and readable result sections
- Short, actionable resume improvement suggestions
- Sample resume and job description content
- Input validation, loading states, retry support, reset, and copy-report actions

## How It Works

1. Paste your resume into the resume field.
2. Paste the target job description into the role field.
3. Click **Analyze my match**.
4. The Flask backend sends the comparison request to the Google Gemini API.
5. Review the match score, matching skills, missing skills, and improvement suggestions.

## Testing

The comparison flow was tested with three different scenarios:

- **High-match scenario** — a resume closely aligned with the role, producing an approximately 85% match.
- **Low-match scenario** — a resume with very little overlap with the role, producing an approximately 5% match.
- **Unrelated-job scenario** — a resume and job description from unrelated fields, confirming that the app surfaces meaningful gaps instead of inventing qualifications.

The API and frontend were also verified independently, including input validation, health checks, production builds, and a real Gemini comparison request.

## Known Limitations

- AI suggestions are directional recommendations, not definitive career or hiring advice.
- Results are most useful when both the resume and job description contain detailed, specific information.
- The app currently analyzes pasted text and does not extract content from uploaded resume files.
- A valid `GEMINI_API_KEY` must be configured in Replit Secrets.
- Google’s current model catalog may not expose `gemini-1.5-flash` for every account. The backend attempts that requested model first and uses a supported Gemini Flash compatibility alias when Google returns a model-not-found response.

## Key Learnings

- Prompt engineering helps guide an AI model toward reliable, structured JSON output.
- API integrations need validation, error handling, retries, and clear user-facing failure states.
- A useful full-stack AI app combines a focused frontend experience with a small, explicit backend contract.

## Live Demo

The app is not currently published to a public demo URL. It can be run and previewed directly in Replit.

**GitHub repository:** [resume-vs-job-match-ai](https://github.com/ezza-fatima380/resume-vs-job-match-ai)