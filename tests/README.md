# LinguaFlow Test Cases

## Test 1: Valid Translation Request

**Payload:** `valid-translation-request.json`

**Purpose:** Verify that a complete translation request is extracted and validated correctly.

### Expected outcome

- The workflow identifies the service as translation.
- The source language is English.
- The target language is Canadian French.
- The deadline and reference number are extracted.
- The request is saved to the jobs data table.
- The request is not sent to manual review.

### How to run

1. Start n8n and Ollama.
2. Open the workflow in n8n and activate or test the webhook as appropriate.
3. Send the JSON payload using Postman to the workflow's webhook URL.
4. Inspect the execution results and confirm the saved record.

**Status:** Not yet verified.