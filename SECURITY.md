# Security Policy

This project may eventually process business conversations and customer contact information. Security and privacy are core requirements.

## Never commit secrets

Do not commit WhatsApp access tokens, Supabase service-role keys, AI API keys, webhook verification secrets, database passwords, or session secrets.

Use environment variables.

## Reporting a vulnerability

Do not create a public GitHub issue for a security vulnerability. Report it privately to the project maintainers with the affected component, reproduction steps, impact, and suggested mitigation if known.

## Data handling

Development and tests should use synthetic data.

Do not upload real customer conversations, phone numbers, access tokens, or production database exports to GitHub.

## Security principles

- Validate external webhook payloads.
- Authenticate webhook requests where supported.
- Validate structured inputs.
- Apply least-privilege credentials.
- Avoid logging secrets or unnecessary customer data.
- Separate human/admin actions from customer-facing AI actions.
- Treat AI output as untrusted input when it can trigger application actions.
