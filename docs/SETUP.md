# Setup and Configuration

## Verified environment

The 173-node workflow structure was checked against n8n 2.22.6. PostgreSQL regression evidence was collected against an isolated PostgreSQL 16 database. Provider operations require separate test accounts and credentials.

## Repository exports

- Recommended candidate: workflows/ai-lead-response-automation-173-node.json
- Historical baseline: ai-lead-response-automation.json (119 nodes)

The candidate export has all n8n credential bindings removed. After import, configure credentials in n8n and bind them to the corresponding nodes. Do not put secrets in workflow JSON or commit them.

## Prerequisites

- n8n 2.22.6 or compatible node versions.
- PostgreSQL 16 for the tested database behavior.
- A dedicated test database and least-privilege role.
- Test Google Sheets account and spreadsheet.
- Test Gmail mailbox.
- Gemini API test credential.
- HTTPS webhook endpoint for any webhook integration test.

## Database prerequisite

The workflow calls PostgreSQL functions and expects the lead response schemas, tables, and transactional functions used by the Task 9H/9J remediation. This repository currently does not contain the complete base schema/bootstrap migration bundle. Do not run the workflow against an empty or production database. Obtain/review the complete migration set before attempting runtime import or execution.

The documented database test results are from the isolated project database; they do not make this repository self-contained.

## Configure the n8n credentials

Create credentials through n8n’s credential store, not in node parameters:

1. PostgreSQL: dedicated isolated database, role, and schema privileges.
2. Google Sheets OAuth: a disposable test spreadsheet only.
3. Gmail OAuth: a test mailbox only.
4. HTTP Header Auth: header name x-goog-api-key with the dedicated Gemini test key as the secret value.

The public export contains no credential bindings. Bind credentials after import; never export credential payloads.

## Workflow configuration fields

Update the Config (EDIT ME) nodes with test-specific values for:

- config.aiApiUrl and config.aiModel
- config.approveSendPath and config.n8nBaseUrl
- config.bookingUrl
- config.errorSheetName, config.sheetId, and config.sheetName
- config.followUp1Days, config.followUp2Days, config.followUp3Days, and config.maxFollowUps
- config.mode and config.timezone
- config.ownerEmail and config.senderEmail

Use example/test addresses and URLs until end-to-end tests are authorized. Do not add the Gemini key as a config field.

## Environment variables

The workflow JSON does not read operating-system environment variables directly. The separate local Compose setup used these variable names; keep actual values in an untracked local .env file:

```dotenv
COMPOSE_PROJECT_NAME=<isolated-project-name>
N8N_ENCRYPTION_KEY=<private-generated-value>
POSTGRES_DB=<isolated-test-database>
POSTGRES_USER=<isolated-test-role>
POSTGRES_PASSWORD=<private-test-password>
```

This repository does not include the Compose project. Never publish the values.

## Import safely

1. Resolve the database migration prerequisite and apply it only to a disposable database.
2. Import the 173-node candidate into an isolated n8n instance as a new workflow.
3. Confirm every workflow credential is bound to a test account.
4. Keep the workflow inactive while validating structure and expressions.
5. Use synthetic leads and a test mailbox; do not trigger the full flow until external calls have been explicitly approved.
6. Review execution retention and redact tokens/personal data from exported evidence.
