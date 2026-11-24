---
name: llm-api-manager
description: Use when the user wants to configure, test, route, or troubleshoot free LLM API endpoints, OpenAI-compatible base URLs, or API keys.
---

# FreeLLMApi Workflow

When helping the user configure or troubleshoot a free LLM API endpoint:

1. **Verify Endpoint & Key Format**
   - Check that the base URL includes the proper protocol (`https://`) and path (such as `/v1`).
   - Never print or log full API keys in plain text; mask all characters except the last 4.

2. **Test Connectivity & List Models**
   - Run a lightweight `curl` request to `<BASE_URL>/models` using the `Authorization: Bearer <API_KEY>` header to confirm connectivity and see available model IDs.

3. **Diagnose Common Errors**
   - **401 Unauthorized**: Verify the header format (`Bearer` vs `x-api-key`) and confirm the key is active.
   - **404 Not Found**: Check if `/v1` needs to be added or removed from the base URL.
   - **429 Rate Limit**: Identify free-tier request-per-minute (RPM) or token-per-day limits and suggest fallback models or retry delays.

4. **Generate Integration Snippet**
   - Provide clean, ready-to-run `curl`, Python (`openai` SDK with custom `base_url`), or environment variable (`ANTHROPIC_BASE_URL` / `OPENAI_BASE_URL`) configuration blocks based on what the user needs.
