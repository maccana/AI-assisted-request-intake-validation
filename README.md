# LinguaFlow — AI-Assisted Translation Request Intake & Validation

## Project Overview

LinguaFlow is a prototype workflow automation system designed to streamline the intake and validation of translation requests for a fictional language services company.

The workflow uses a locally hosted large language model (LLM) to extract structured information from incoming requests, applies validation rules to identify missing information, and routes requests to the appropriate data table for processing or manual review.

The project demonstrates how AI and workflow automation can reduce repetitive administrative work while keeping incomplete or ambiguous requests visible for human review.

## Workflow Overview

![LinguaFlow n8n workflow showing request intake, AI extraction, validation, and routing to storage or manual review](docs/workflow-overview.png)

The workflow follows these steps:

1. **Receive request:** Accepts an incoming translation request through an n8n webhook.
2. **Prepare request:** Combines the subject and body into a single text input and preserves the sender's email address.
3. **Extract job details:** Uses a locally hosted LLM through Ollama to extract structured information from the request.
4. **Parse AI response:** Converts the model's JSON response into structured fields.
5. **Validate request:** Checks whether required information is present, including the service type and source language. Translation requests must also include a target language.
6. **Route request:** Saves valid requests to the main data table and routes incomplete requests to a review table.

## Technology Stack

- **n8n:** Workflow automation and orchestration
- **Ollama:** Local LLM execution
- **Llama 3.1 8B:** Information extraction from incoming requests
- **n8n Data Tables:** Storage of accepted requests and requests requiring review
- **Webhook:** Entry point for incoming requests

## Current Capabilities

- Extracts structured information from unstructured request text.
- Captures service type, source and target languages, deadlines, urgency, quote requests, reference numbers, and additional details.
- Preserves the original request text for traceability.
- Applies validation rules before routing requests.
- Separates accepted requests from requests requiring manual review.
- Uses a locally hosted LLM rather than sending request text to a hosted LLM API.

## Known Limitations

- The LLM may incorrectly infer a service type when the request is ambiguous.
- The validation rules depend on the accuracy of the information extracted by the model.
- Deadline parsing and timezone handling require further validation.
- Requests routed for review currently receive a general review reason rather than a detailed explanation of every missing field.
- The workflow is a prototype and has not been established as a production-ready system.

## Project Status

The initial prototype is implemented, with the core intake, extraction, validation, and routing workflow in place.

Further work will focus on documenting test results, improving reproducibility, and evaluating the reliability of AI-based extraction and validation.

## Privacy and Security

The project uses a fictional company name and is intended as a portfolio demonstration.

The workflow is designed around local LLM execution through Ollama. However, local inference alone does not guarantee complete data privacy or security; deployment configuration, access controls, logging, and data storage must also be considered.

Before reusing or deploying the workflow, configure the required n8n credentials, data tables, and local Ollama connection. Review all configuration and sample data before using the workflow with real client information.

## Setup and Configuration

### Prerequisites

Before running LinguaFlow, ensure you have the following installed and running:

- **Docker Desktop** — runs the n8n container.
- **n8n** — the workflow automation platform.
- **Ollama** — runs the local language model.
- **Llama 3.1 8B** — the model used for extracting structured information from requests.

Ollama is available locally at `http://localhost:11434/`

The n8n workflow connects to Ollama through Docker Desktop using `http://host.docker.internal:11434/`.

### Model Configuration

LinguaFlow uses the `llama3.1:8b` model through Ollama. Ensure the model is available locally before running the workflow.

To check that the model is available, run this command in a terminal:

```bash
ollama list
```

If the model is not listed, download it using:

```basg
ollama pull llama3.1:8b
```

### Importing the Workflow

1. Open your n8n instance.
2. Open the workflow menu and select **Import from File**.
3. Select `linguaflow-request-intake-validation.json` from the project repository.
4. Configure the Ollama credentials and select the appropriate data tables.
5. Save the workflow.

**Note:** The imported workflow requires configuration before it can run. Verify the credential settings and data table references in your n8n instance.

### Testing the Workflow

1. Activate the workflow in n8n or use its test mode, as appropriate.
2. Send a sample translation request to the workflow's webhook using Postman.
3. Check the `LinguaFlowJobs` data table for valid requests.
4. Check the `LinguaFlowReview` data table for requests that are missing required information.

Use fictional request data when testing. Confirm that complete requests are saved as jobs and incomplete requests are routed for manual review.