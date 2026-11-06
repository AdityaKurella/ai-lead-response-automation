# AI Lead Response Automation

A 119-node n8n workflow for capturing and qualifying inbound leads, generating a response draft, routing it through owner approval, and coordinating follow-up and reply/status handling.

## Included workflow

- `ai-lead-response-automation.json` — combined 119-node workflow export.

## Requirements

- n8n with Google Sheets, Gmail, webhook, and HTTP Request nodes.
- Google Gemini API access for the HTTP-based AI calls.
- A Google Sheet matching the columns referenced in the workflow.

## Import and configure

1. Import the workflow JSON into n8n.
2. Assign your own Google Sheets and Gmail credentials. Credential bindings were removed from this sanitized export.
3. Configure the Gemini HTTP authentication credential, Google Sheet references, owner notification address, booking URL, and n8n base URL.
4. Review webhook paths, approval-token handling, follow-up schedule, email content, and Gmail trigger settings.
5. Test with a dedicated sheet and test mailbox before enabling any automatic send path.

## Notes

Deployment URLs and sheet/owner identifiers are placeholders. This is a workflow export and does not include a spreadsheet, API key, credentials, or deployed webhooks. Review all sending and consent behavior before activation.

