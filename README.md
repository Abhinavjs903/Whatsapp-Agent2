# WhatsApp Business Agent

> An open-source, business-configurable WhatsApp AI agent being developed under **Quant Tech**.

WhatsApp Business Agent is a planned automation platform for small businesses and teams that want to handle customer conversations, lead capture, bookings, FAQs, follow-ups, and human handoff from WhatsApp.

The project is intentionally being built as a **business-configurable engine**, not as a single-purpose chatbot. A business should be able to define its services, FAQs, operating hours, booking rules, reply style, escalation rules, and automation workflows without rewriting the core agent.

## Status

🚧 **Early-stage / architecture phase**

The repository contains the project specification and contribution structure. The implementation will be developed incrementally through GitHub issues.

## What we're building

### Core conversation flow

`Customer → WhatsApp → Webhook → Agent Engine → Business Configuration + Data → Response`

The agent should be able to:

- Answer business FAQs
- Understand common customer intents
- Capture and qualify leads
- Provide service/product information
- Handle appointment or booking requests
- Collect structured customer details
- Trigger follow-ups and reminders
- Escalate conversations to a human
- Pause automation when a human takes over
- Keep business-specific rules separate from the core agent
- Produce structured logs for debugging and analytics

### Example

A customer sends:

> "Hi, I want to book a haircut for tomorrow evening."

The agent should be able to:

1. Detect the booking intent.
2. Identify the requested service.
3. Check business availability.
4. Ask for missing information.
5. Confirm the appointment.
6. Store the booking.
7. Send a confirmation.
8. Trigger a reminder workflow later.

If the request is outside the configured automation scope, the agent should hand the conversation to a human instead of inventing an answer.

## Planned architecture

```text
                         ┌──────────────────┐
                         │ WhatsApp Business │
                         │      API         │
                         └────────┬─────────┘
                                  │
                                  ▼
                         ┌──────────────────┐
                         │ Webhook / API    │
                         │    Layer         │
                         └────────┬─────────┘
                                  │
                                  ▼
                    ┌──────────────────────────┐
                    │      Agent Engine        │
                    │                          │
                    │ Intent → Context → Rules │
                    │ → AI → Action → Response │
                    └───────┬──────────┬───────┘
                            │          │
                 ┌──────────┘          └──────────┐
                 ▼                                ▼
        ┌─────────────────┐              ┌─────────────────┐
        │ Business Config │              │   Data Store    │
        │ FAQs            │              │ Leads           │
        │ Services        │              │ Conversations   │
        │ Hours           │              │ Bookings        │
        │ Policies        │              │ Settings        │
        └─────────────────┘              └─────────────────┘
                            │
                            ▼
                   ┌─────────────────┐
                   │ Automation Layer│
                   │ Reminders       │
                   │ Follow-ups      │
                   │ Notifications   │
                   └─────────────────┘
                            │
                            ▼
                   ┌─────────────────┐
                   │ Human Handoff   │
                   │ / Bot Paused    │
                   └─────────────────┘
```

## Initial technology direction

The initial implementation is planned around:

- **Backend:** Node.js + TypeScript + Express
- **Database:** Supabase / PostgreSQL
- **WhatsApp:** WhatsApp Cloud API
- **AI:** Provider-agnostic AI integration
- **Automation:** Webhook/event based workflows, with optional n8n/Make integrations
- **Testing:** Unit + integration tests
- **Deployment:** Container/cloud friendly

These are implementation targets, not a claim that all integrations are already implemented.

## Business configuration

The core engine should not contain hard-coded business logic.

Example conceptual configuration:

```json
{
  "business": {
    "name": "Example Salon",
    "timezone": "Asia/Kolkata"
  },
  "services": [
    {
      "name": "Haircut",
      "duration_minutes": 45
    }
  ],
  "hours": {
    "monday": ["10:00", "20:00"]
  },
  "automation": {
    "lead_capture": true,
    "booking": true,
    "follow_up": true
  },
  "handoff": {
    "enabled": true,
    "keywords": ["human", "agent", "support"]
  }
}
```

The exact schema will evolve through contributor issues.

## Planned project structure

```text
Whatsapp-Agent2/
├── backend/
│   ├── src/
│   │   ├── api/
│   │   ├── agent/
│   │   ├── config/
│   │   ├── integrations/
│   │   ├── services/
│   │   ├── db/
│   │   └── utils/
│   └── tests/
├── docs/
│   ├── architecture.md
│   └── product-spec.md
├── .github/
│   └── ISSUE_TEMPLATE/
├── .env.example
├── CONTRIBUTING.md
├── SECURITY.md
└── README.md
```

## Roadmap

### Phase 1 — Foundation
- [ ] Repository and architecture setup
- [ ] TypeScript backend
- [ ] Health endpoint
- [ ] Environment/config system
- [ ] Supabase database schema
- [ ] Basic webhook abstraction

### Phase 2 — WhatsApp
- [ ] WhatsApp webhook verification
- [ ] Incoming message normalization
- [ ] Outgoing message service
- [ ] Message status handling
- [ ] Error/retry strategy

### Phase 3 — Agent Engine
- [ ] Intent model
- [ ] Business context loader
- [ ] FAQ answering
- [ ] Structured tool/action interface
- [ ] Guardrails
- [ ] Conversation state

### Phase 4 — Business Automation
- [ ] Lead capture
- [ ] Booking flow
- [ ] Follow-up engine
- [ ] Reminder events
- [ ] Human handoff / bot pause
- [ ] Conversation history

### Phase 5 — Developer Experience
- [ ] Tests
- [ ] CI
- [ ] API documentation
- [ ] Example business configuration
- [ ] Local development guide
- [ ] Observability/logging

### Phase 6 — Extensions
- [ ] n8n integration
- [ ] Additional AI providers
- [ ] CRM integrations
- [ ] Analytics
- [ ] Admin dashboard

## Contributing

This project is being prepared as a **Quant Tech open-source project**.

Start with an issue before implementing a non-trivial change. See [CONTRIBUTING.md](CONTRIBUTING.md).

Good contribution areas include:

- Backend/API
- AI/agent logic
- WhatsApp integration
- Database design
- Automation
- Testing
- Documentation
- Developer tooling
- Security
- Observability

Beginner-friendly issues will be marked with `good first issue`.

## Design principles

1. **Business-configurable:** business behavior belongs in configuration/data, not scattered through code.
2. **Safe by default:** the agent must not fabricate bookings, prices, policies, or availability.
3. **Human override:** businesses must be able to take over conversations.
4. **Provider separation:** AI and automation providers should be replaceable.
5. **Testable:** agent decisions and business rules should be testable without a live WhatsApp account.
6. **Privacy-aware:** secrets and customer data must never be committed to the repository.
7. **Small PRs:** contributors should make focused, reviewable changes.

## Security

Never commit:

- WhatsApp access tokens
- Supabase credentials
- AI API keys
- Webhook secrets
- Customer phone numbers or conversation exports

See [SECURITY.md](SECURITY.md).

## License

License will be finalized before the first public release.
