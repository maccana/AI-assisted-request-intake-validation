# LinguaFlow Test Cases

This directory contains sample JSON payloads for testing the LinguaFlow workflow.

The tests verify that incoming translation requests are correctly processed, validated, and routed according to the information provided.

## Test 1: Valid Translation Request

**Payload:** `payloads/01-valid-translation-request.json`

**Purpose:** Verify that a complete translation request is extracted and validated correctly.

**Expected outcome:**
- Service type is identified as translation.
- Source language is English.
- Target language is Canadian French.
- Deadline and reference number are extracted.
- Quote request is correctly identified.
- Request is saved to the valid jobs data table.
- Request is not sent for manual review.

**Status:** Passed

## Test 2: Missing Target Language

**Payload:** `payloads/02-missing-target-language.json`

**Purpose:** Verify that an incomplete translation request is identified and routed for manual review.

**Expected outcome:**
- Service type is identified as translation.
- Source language is German.
- Target language is missing.
- Request is routed to the review branch.
- Request is saved to the review data table.
- Request is not saved to the valid jobs table.

**Status:** Passed

## How to Run the Tests

1. Start n8n and Ollama.
2. Open the imported LinguaFlow workflow.
3. Start the workflow's webhook test listener, or activate the workflow if using its production webhook.
4. Send the selected JSON payload using Postman.
5. Inspect the execution results and verify that the request follows the expected route.
6. Check the corresponding data table to confirm that the record was saved correctly.

**Note:** These test cases use the flat JSON request format expected by the current webhook.