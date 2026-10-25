# ContextHop

**Hit your limit on Claude? Continue the same work on ChatGPT, Gemini, or any other model - without explaining everything from the beginning.**

ContextHop turns a finished (or interrupted) AI conversation into one portable `HANDOFF.md` file: a starter prompt for the new model + a clean, structured copy of your context. Paste it, and the new model picks up where the old one stopped.

No API key. No account. No server. 100% local and free.

## The problem

You spend an hour building something with one AI. Then: *"You've reached your limit."*
You open another model and waste 20 minutes re-explaining the goal, the decisions, the code, and what already failed.

Your context should travel with **you**, not stay locked inside one app.

## Two ways to use it

### Way 1 - The Magic Prompt (zero install, works on mobile)

Before your limit runs out, paste the prompt in [`prompts/magic_handoff_prompt.md`](prompts/magic_handoff_prompt.md) as your last message on the old model. It writes its own handoff summary. Paste that summary into the new model. Done.

### Way 2 - The Python tool

```bash
git clone https://github.com/aryancodes-dev/contexthop.git
cd contexthop
python context_hop.py your_chat.txt
# creates HANDOFF.md - fill the 3 [EDIT ME] lines, then paste/upload it in the new model
```

Works with transcripts exported or copied from ChatGPT, Claude, Gemini, DeepSeek and Perplexity (lines starting with `User:` / `Claude:` / etc.).

Try the example:

```bash
python context_hop.py examples/sample_chat.txt
```

## Why not just copy-paste the whole chat?

| | Full copy-paste | ContextHop handoff |
|---|---|---|
| Tokens on new model | 20,000+ | ~500-1,500 (Magic Prompt) |
| New model understands state | Has to dig through chat | Goal / decisions / next step up top |
| Works when limit already hit | Yes, but messy | Yes - transcript mode |

## Roadmap

- [x] v0.1 - Python CLI + Magic Prompt
- [ ] v0.2 - Auto-detect ChatGPT / Claude JSON exports
- [ ] v0.3 - Simple web page version (paste chat -> download HANDOFF.md)
- [ ] v0.4 - Browser extension (one-click export)

## Contributing

Issues and PRs welcome. Especially: export parsers for new platforms, and translations of the Magic Prompt.

## License

MIT - see [LICENSE](LICENSE).
