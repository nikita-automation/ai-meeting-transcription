# AI Meeting Transcription

AI Meeting Transcription is an automation project for converting recorded meetings into transcripts, summaries, action items, and structured follow-up records. The system is designed for teams that want to reduce manual note-taking while keeping human review in the process. It uses a workflow automation layer to move audio files through transcription, AI analysis, structured storage, and review.

## Project Overview

This project demonstrates a practical AI automation architecture for meeting documentation. A recorded meeting is uploaded to a cloud folder or submitted through a webhook. The workflow transcribes the audio, generates a structured summary, extracts decisions and action items, and stores the output in a reviewable format.

The implementation is intentionally tool-agnostic where appropriate. The workflow can be implemented in n8n or Make.com, with OpenAI and Whisper-compatible transcription services used for the AI processing steps. The repository includes documentation, diagrams, and an example workflow export that can be adapted for a real deployment.

## Business Problem

Meeting notes are often incomplete, inconsistent, or delayed. Participants may forget decisions, miss follow-up tasks, or rely on manual notes that do not capture the full discussion. In teams with frequent calls, this creates repeated administrative work and makes it difficult to maintain a reliable record of outcomes.

The problem becomes more visible when meetings include customers, project stakeholders, or cross-functional teams. Action items need owners and deadlines, decisions need to be documented, and summaries need to be shared quickly. Manual transcription and summarization are possible, but they do not scale well and often depend on one person's availability.

## Solution

The automation processes meeting recordings through a repeatable workflow. Audio files are collected from a defined input location, sent to a transcription step, analyzed with an AI model, and written into structured outputs for human review. The workflow separates raw transcript generation from higher-level meeting analysis so each stage can be inspected and improved independently.

The system does not replace human judgment. It creates a first-pass transcript and meeting report that can be reviewed, corrected, and shared. This keeps the automation useful for real business workflows while avoiding over-reliance on AI-generated text.

## Architecture

```text
Meeting Recording
  ↓
Google Drive / Webhook
  ↓
n8n / Make.com
  ↓
Whisper Transcription
  ↓
OpenAI Analysis
  ↓
Google Docs / Google Sheets
  ↓
Human Review
  ↓
Follow-up Actions
```

## Workflow

1. A meeting recording is uploaded to a monitored folder or submitted through a webhook.
2. The automation validates the file type and stores metadata such as file name, upload time, and source link.
3. The audio file is sent to a transcription service such as Whisper.
4. The transcript is saved as a separate text artifact or document.
5. The transcript is sent to OpenAI with structured instructions for meeting analysis.
6. The AI step produces a concise summary, key discussion points, decisions, risks, open questions, and action items.
7. The workflow maps the AI output into a structured report.
8. The report is saved to Google Docs or Google Sheets for review.
9. The original record is updated with processing status, transcript link, and report link.
10. Failed steps are logged with clear error messages for manual inspection.

## Technologies

| Technology | Purpose |
| --- | --- |
| n8n / Make.com | Workflow orchestration |
| Whisper | Audio transcription |
| OpenAI | Summary and action item extraction |
| Google Drive | Meeting recording storage |
| Google Docs | Human-readable meeting report |
| Google Sheets | Structured tracking and review |
| Webhooks | External submission endpoint |
| HTTP API | Service-to-service integration |

## Features

- Audio file intake from folder or webhook
- Automated meeting transcription
- AI-generated summaries and structured notes
- Extraction of decisions, risks, open questions, and action items
- Links between original recording, transcript, and report
- Human review stage before sharing or operational use
- Error handling for missing files and failed API requests
- Modular design suitable for n8n or Make.com implementation

## Repository Structure

```text
AI-Meeting-Transcription/
├── README.md
├── LICENSE
├── .gitignore
├── assets/
│   └── workflow.png
├── workflows/
│   └── workflow.json
├── docs/
│   ├── architecture.md
│   └── implementation.md
└── diagrams/
    └── architecture.png
```

## Screenshot

![Workflow](assets/workflow.png)

## Future Improvements

- Add speaker diarization when supported by the transcription provider
- Add automatic assignment of action items to owners
- Integrate with project management tools such as Jira, Trello, or Asana
- Add approval workflow before reports are shared
- Add multilingual transcript handling
- Add retention policies for sensitive recordings and transcripts
- Add alerting for failed or incomplete processing runs
