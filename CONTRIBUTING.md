# Contributing to WhatsApp Business Agent

Thank you for contributing to the Quant Tech WhatsApp Business Agent.

The project is currently in its architecture/foundation phase, so contributions should focus on building a clean base rather than adding isolated features.

## Before you start

1. Read the issue completely.
2. Comment on the issue describing your intended approach.
3. Wait for maintainers to confirm the scope for non-trivial changes.
4. Fork the repository.
5. Create a focused branch.
6. Make the smallest complete change that solves the issue.
7. Add or update tests where applicable.
8. Update documentation when behavior changes.
9. Open a pull request referencing the issue.

## Branch naming

Use:

```text
feat/<short-name>
fix/<short-name>
docs/<short-name>
test/<short-name>
refactor/<short-name>
chore/<short-name>
```

## Commit messages

Prefer conventional-style commits:

```text
feat: add message normalizer
fix: handle invalid webhook payload
docs: document business configuration
test: add booking service tests
refactor: isolate agent context
chore: add lint configuration
```

## Pull requests

Every PR should:

- Explain what changed.
- Explain why it changed.
- Reference the related issue.
- Include testing performed.
- Avoid unrelated refactors.
- Avoid secrets or real customer data.
- Keep configuration changes documented.

Suggested PR format:

```markdown
## What changed

-

## Why

-

## Testing

-

## Related issue

Closes #123
```

## Architecture rules

### Keep business logic configurable

Do not hard-code business names, prices, hours, services, FAQs, booking policies, or escalation contacts.

### Separate AI from deterministic logic

The LLM should help with language understanding and response generation. Deterministic operations such as booking creation, availability checks, lead storage, business hours, and state transitions should be explicit application logic/tools.

### Never let the model invent system state

The agent must not claim that a booking exists, a slot is available, a payment succeeded, or a human was notified unless the application has verified that state.

### Keep integrations replaceable

WhatsApp, AI providers, databases, and automation tools should sit behind clear interfaces where practical.

## Testing expectations

Contributors should test:

- normal input
- malformed input
- missing fields
- external API failures
- duplicate events where relevant
- authorization/security boundaries
- human handoff behavior

AI features should include deterministic tests around the surrounding application logic wherever possible.

## Good first contributions

- Add request validation
- Improve webhook error handling
- Add unit tests
- Improve documentation
- Add sample business configuration
- Add message normalization utilities
- Add structured logging
- Add CI checks

## Discuss first

Please discuss an issue before large PRs for database schema changes, major architecture changes, new external providers, authentication/authorization, agent safety behavior, or large dashboard work.

## Code review

Reviewers will primarily look for correctness, security, simplicity, testability, architectural compatibility, and documentation.

A technically working PR may still be asked to change if it makes the project harder to maintain.

## Community

Be respectful, specific, and technical. The goal is to build a maintainable open-source project together.
