# Architecture

The public [workflow export](../workflow/demo-a-sanitized.json) contains the visual n8n nodes and connections. It preserves the core logic while replacing credential and runtime identifiers with placeholders.

1. **Intake and validation:** webhook input is normalized and checked for required fields. Invalid inputs go to review rather than confirmed CRM status.
2. **Deduplication:** normalized email and company are checked before the AI call. Normal sequential repeats return the prior lead instead of calling Gemini again.
3. **Qualification:** a real Gemini API call requests structured `fit`, `score`, `confidence`, `reason`, and `missing_info`. The workflow validates types and ranges independently.
4. **Routing:** unclear or invalid results wait for review. Other qualified results are stored in an n8n Data Table, used as a CRM-style persistence layer in this demo.
5. **After persistence:** a high-value notification is mocked; the follow-up is saved as `draft_only` and never auto-sent.
6. **Failure handling:** errors retain their stage for inspection. Explicit retry paths were tested for AI and downstream CRM failures.

This is a local portfolio implementation. The n8n tests cover normal repeated submissions, not an enterprise exactly-once guarantee for concurrent requests.
