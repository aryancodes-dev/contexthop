# The Magic Handoff Prompt (no tool needed)

**When to use:** BEFORE your tokens / limit run out on the old model,
paste this as your last message there. The old model summarises itself -
that costs far fewer tokens on the new model than pasting the whole chat.

---

Copy from here:

```
I am switching to another AI model to continue this work.
Create a HANDOFF SUMMARY of our entire conversation so far, in Markdown,
with exactly these sections:

1. GOAL - what I am ultimately trying to achieve (2-3 lines)
2. DONE SO FAR - what is completed, in order
3. KEY DECISIONS - choices we made and WHY
4. CODE / FILES - any important code, file names, or data (copy them exactly)
5. PROBLEMS - errors or things that did not work
6. NEXT STEP - the single next thing to do
7. RULES - my preferences / instructions you must keep following

Be complete but short. Do not add new ideas. Do not ask me questions.
```

Then: copy its reply, paste it as your FIRST message in the new model,
with this line on top:

```
Continue from this handoff. First confirm in 3 lines where we are,
then do the NEXT STEP.
[HANDOFF SUMMARY PASTED HERE]
```

---

**Why this works:** a full transcript can be 20,000+ tokens of "Sure!",
"Great question!" and dead ends. A good handoff is usually 500-1,500
tokens - and the new model actually understands the *state* of the work,
not just the words.
