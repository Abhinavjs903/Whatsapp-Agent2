# Product Specification

## Problem

Small businesses often receive repetitive WhatsApp questions and leads but still handle most conversations manually.

The project aims to automate repetitive communication while keeping businesses in control.

## Primary use cases

### FAQ automation

Customer asks what the business timings are. The agent answers from configured business data.

### Lead capture

When a customer expresses buying intent, the agent collects configured fields such as name, requirement, preferred service, and preferred time.

### Booking

When a customer requests an appointment, the agent checks the configured availability before confirming anything.

### Follow-up

A lead that becomes inactive can trigger a follow-up according to business rules.

### Human handoff

A customer can request a human or trigger an escalation condition. The agent then pauses and routes the conversation to the configured human workflow.

## Product constraints

- Business-specific information must come from trusted configuration/data.
- AI should not directly mutate important state without validated application actions.
- Every automated action should be observable.
- Customers should have a clear path to human assistance.

## MVP boundary

The MVP should support:

1. Incoming WhatsApp message
2. Business configuration
3. FAQ response
4. Basic intent detection
5. Lead capture
6. Booking flow
7. Human handoff
8. Persistent conversation state
9. One automation/follow-up mechanism
10. Tests for the above
