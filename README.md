# ClarityAI

> **Status: early design sketch — not yet implemented.**
> This repository currently contains the intended module layout and design notes.
> There is no working code here yet. See [Roadmap](#roadmap) for what's planned.

An AI assistant that lives directly inside an SMS/iMessage group chat. The idea: rather
than making people leave the conversation to look something up or settle a disagreement,
the bot participates in the thread — answering questions, summarizing what was decided,
and helping the group converge when planning something.

## Planned architecture

| Module | Responsibility |
|---|---|
| `src/main.py` | FastAPI endpoints; inbound webhook handling from the SMS provider (Twilio) |
| `src/agent.py` | Prompt construction and LLM response generation |
| `src/memory.py` | Short-term conversation buffer, plus longer-term recall across threads |
| `src/models.py` | Database schema for messages, threads, and participants |

**Intended stack:** Python, FastAPI, Twilio (SMS/iMessage gateway), an LLM API for
generation, and a persistence layer for conversation memory.

## Design notes

The interesting problems in a group-chat agent aren't the LLM call — they're around it:

- **When to speak.** A bot in a group thread that replies to everything is unusable. It
  needs to decide whether a given message is addressed to it or warrants interjection.
- **Context windowing.** Group chats are long-running and multi-participant. Short-term
  buffer plus retrieval over older history, rather than replaying the whole thread.
- **Speaker attribution.** Responses have to track who said what to be useful for
  summarizing decisions or resolving a dispute about what was agreed.

## Roadmap

- [ ] Twilio webhook receiver and message ingestion
- [ ] Conversation store and schema
- [ ] Short-term buffer with retrieval over history
- [ ] Addressed-to-bot detection
- [ ] LLM response generation
- [ ] Thread summarization

## Running

Nothing to run yet.
