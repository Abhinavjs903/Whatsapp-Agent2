# Architecture

## Goal

Build a reusable WhatsApp business-agent engine where the same core system can support different businesses through configuration.

## Message lifecycle

```text
Incoming WhatsApp event
        ↓
Webhook validation
        ↓
Message normalization
        ↓
Conversation lookup
        ↓
Business configuration
        ↓
Intent / context analysis
        ↓
Guardrails
        ↓
Tool or response decision
        ↓
Deterministic business action
        ↓
Response generation
        ↓
WhatsApp delivery
        ↓
Event/log persistence
```

## Agent layers

### 1. Transport

Receives and sends WhatsApp messages. It should not contain business rules.

### 2. Normalization

Converts provider-specific payloads into an internal message format.

```ts
type IncomingMessage = {
  messageId: string;
  senderId: string;
  text?: string;
  timestamp: string;
  type: string;
};
```

### 3. Context

Loads business configuration, conversation history, customer state, relevant FAQs/services, and workflow state.

### 4. Intent and decision layer

Initial intents:

- faq
- service_information
- lead_capture
- booking
- booking_change
- cancellation
- follow_up
- human_handoff
- unknown

### 5. Tools/actions

The agent requests explicit application actions such as:

```text
create_lead
check_availability
create_booking
cancel_booking
schedule_followup
handoff_to_human
```

The application executes and verifies the action.

### 6. Response

Only after the action/result is known should the final customer response be generated.

## Human handoff

```text
BOT_ACTIVE → BOT_PAUSED → HUMAN_ACTIVE → BOT_RESUMED
```

When `BOT_PAUSED` is active, normal automated replies should not be sent.

## Automation

Automation should be event-driven.

```text
lead.created
booking.created
booking.cancelled
conversation.inactive
followup.due
human.handoff
```

This allows integrations such as n8n/Make to be added without coupling the core agent to one automation provider.

## Initial data entities

- businesses
- business_settings
- customers
- conversations
- messages
- leads
- services
- bookings
- automation_events

## Non-goals for the first version

The first version should not attempt to become a full CRM, unrestricted autonomous agent, replacement for WhatsApp Business, payment processor, or general-purpose workflow platform.
