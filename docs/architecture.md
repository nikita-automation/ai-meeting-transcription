# Architecture

## Overview

The AI Meeting Transcription workflow is designed as a staged automation pipeline. Each stage has a clear responsibility: intake, validation, transcription, AI analysis, report generation, and review. This separation makes the workflow easier to debug and safer to operate because intermediate outputs can be inspected before the final report is used.

## System Diagram

```text
Meeting Recording
  ↓
Input Layer
  - Google Drive folder
  - Webhook upload
  ↓
Automation Layer
  - n8n or Make.com
  - Validation
  - Status tracking
  ↓
Transcription Layer
  - Whisper-compatible service
  ↓
Analysis Layer
  - OpenAI summary
  - Decisions
  - Action items
  - Risks
  ↓
Output Layer
  - Google Docs report
  - Google Sheets tracking row
  ↓
Human Review
```

## Main Components

### Input Layer

The input layer receives meeting recordings from a controlled source. A monitored Google Drive folder is useful for internal teams, while a webhook is useful when recordings are submitted from another application.

### Automation Layer

n8n or Make.com coordinates the workflow. This layer validates files, sends API requests, maps responses, stores status updates, and manages errors.

### Transcription Layer

The transcription step converts audio into text. The output should be stored separately from the AI summary so reviewers can compare the generated report with the original transcript.

### Analysis Layer

OpenAI receives the transcript and returns structured meeting notes. The prompt should request predictable sections so downstream tools can map the output into documents or spreadsheet fields.

### Output Layer

The final outputs are stored in reviewable systems such as Google Docs and Google Sheets. This keeps the automation practical for business use because humans can validate and edit the result.
