# Security and Data Handling

## Credentials

- Store Gemini, Gmail, Google Sheets, and PostgreSQL credentials in n8n’s credential store.
- Never paste an API key, OAuth token, password, or bearer token into workflow JSON, a URL, a sheet, or this repository.
- The public 173-node export has all n8n credential references removed. Rebind only isolated test credentials after import.
- Do not commit .env files, credential exports, execution payloads, customer data, or private keys.

## Approval and delivery controls

The remediation design uses cryptographically secure approval tokens, stores token hashes in the transactional store, enforces expiration, and consumes approvals atomically. Approval requires explicit confirmation. The database outbox and conditional claims are designed to prevent concurrent duplicate processing.

Delivery and Google Sheets synchronization are separate states. A successful email must not be resent just because Sheets synchronization failed. Ambiguous email outcomes require reconciliation; they are not automatically retried.

These controls have database-level and synthetic test evidence. The full n8n workflow and live provider paths have not been verified end to end.

## Historical 119-node export

The preserved 119-node baseline has a placeholder Gemini key header whose name includes trailing whitespace. It contains no recognized live Google API key pattern, but it is not the recommended import artifact. Do not replace its placeholder with a real key. Use the credential-based 173-node candidate after reviewing its pending engine verification.

## Public-data review

The published workflow exports contain no n8n credential payloads, recognized Google API key patterns, private-key blocks, or customer records. Example email addresses use example.com. Continue scanning every export and report before publishing changes.
