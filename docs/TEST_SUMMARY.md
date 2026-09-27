# Test Summary

The local **real-Gemini n8n workflow** passed **10/10 test scenarios** on 26 September 2026 with fictional leads. Eight successful real Gemini API calls were recorded during validation. The outcomes below come from the local test report; raw execution data and credential-related error payloads are intentionally excluded.

| Scenario | Observed outcome |
| --- | --- |
| High-fit lead | Structured Gemini result validated; one CRM-style record and draft-only follow-up |
| Low-quality lead | Real Gemini classification routed by the configured rules |
| Low-information lead | `review_pending`; no confirmed CRM record |
| Invalid input | Review path; no Gemini call |
| Authentication failure | Visible `ai_call` error; no CRM write |
| Network failure | Visible `ai_call` error; no CRM write |
| Malformed structured output | Rejected by validation; review path |
| Retry after AI failure | Recovered with one successful real Gemini call and one CRM record |
| Downstream CRM retry | CRM write recovered without another LLM call |
| Normal duplicate submission | `duplicate=true`; no second Gemini call or CRM row |

The destination table was checked for duplicate lead IDs. The test-only failure paths did not alter a live client system. Concurrent duplicate submissions were not established for this n8n implementation; a separate Node.js simulator result is not attributed to n8n.
