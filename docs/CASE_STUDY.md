# Public Case Study — Website Enquiry Qualification in n8n

*Portfolio demo with fictional data; the CRM in the demo is an n8n Data Table and the alert is mocked.*

## The problem

Small B2B service teams often read website enquiries manually, decide which ones look promising, and copy them into a CRM. Repeated submissions, incomplete fields, uncertain qualification, and failed steps make that process hard to trust. This demo explores a clearer route from form submission to a reviewable record.

## The build

I built a visual n8n workflow that receives a webhook enquiry, normalizes and validates its fields, and checks the combination of normalized email and company before qualification. A real Google Gemini call returns structured fit, score, confidence, reason, and missing-information fields. The workflow independently checks that response instead of trusting the model output. Low-confidence, incomplete, or invalid results go to human review.

Qualified leads are recorded in the Data Table. A follow-up is kept as `draft_only`; no email is sent. Failed stages are visible and can be retried within the demonstrated workflow.

## Evidence

The local real-LLM version passed **10/10 test scenarios**. The scenarios included high-fit and incomplete enquiries, invalid input, a repeat submission before a second AI call, malformed model output, simulated service failures, and retry. The destination table was checked for duplicate lead IDs. The n8n workflow was tested for sequential duplicates; its concurrent behaviour was not established by these tests.

## Client use

A client engagement would require their own accounts, a written scope, privacy review, integration-specific tests, and acceptance before use with real data.

*Detailed local test evidence is available on request.*
