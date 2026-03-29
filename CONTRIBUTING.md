# Contributing to E.C.H.O.

Thanks for your interest in contributing.

## How to Contribute

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/your-feature`)
3. Make your changes
4. Commit (`git commit -m 'Add your feature'`)
5. Push (`git push origin feature/your-feature`)
6. Open a Pull Request

## What to Contribute

- **Prompt improvements** — Better narrative generation, tighter role definitions, smarter crossweave logic
- **Documentation** — Clearer guides, examples, translations of the guides
- **Bug reports** — If the prompt produces inconsistent output, broken formatting, or loses state
- **Session reports** — Played a session? Share what worked and what didn't

## Guidelines

- Keep all internal systems (state, commands, labels, code) in English
- Player-facing narrative output should remain multilingual
- Test prompt changes by running a full session (at least 3 players, 3 rounds)
- Keep the tone sharp and grounded — no spiritual or esoteric language

## Reporting Issues

Open an issue with:
- The LLM you used (Claude, ChatGPT, Gemini, etc.)
- The command or phase where the issue occurred
- What you expected vs. what happened
- The `/state` dump if available
