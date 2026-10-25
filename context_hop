#!/usr/bin/env python3
"""
ContextHop - Carry an AI chat to any other model without starting over.

Usage:
    python context_hop.py sample_chat.txt
    python context_hop.py sample_chat.txt -o HANDOFF.md
    python context_hop.py sample_chat.txt --goal "Build a resume website"

Input: a plain .txt / .md chat transcript. Works best if lines start with
       "User:" / "You:" / "Assistant:" / "ChatGPT:" / "Claude:" / "Gemini:"
       If no labels are found, the whole file is treated as raw transcript.

Output: a HANDOFF.md file containing
  1. A ready-to-paste starter prompt for the NEW model
  2. A structured context section (goal, transcript cleaned up)
  3. The full original transcript (so nothing is lost)

No API key. No internet. 100% local.
"""
import argparse
import re
import sys
from datetime import date
from pathlib import Path

SPEAKERS = r"(User|You|Human|Assistant|ChatGPT|Claude|Gemini|DeepSeek|Perplexity|AI)"
LINE_RE = re.compile(rf"^\s*{SPEAKERS}\s*:\s*", re.IGNORECASE)


def parse_transcript(text: str):
    """Split a transcript into (speaker, message) turns."""
    turns = []
    current_speaker, current_lines = None, []
    for line in text.splitlines():
        m = LINE_RE.match(line)
        if m:
            if current_speaker is not None:
                turns.append((current_speaker, "\n".join(current_lines).strip()))
            current_speaker = m.group(1).title()
            current_lines = [line[m.end():]]
        else:
            if current_speaker is None:
                current_speaker, current_lines = "User", []
            current_lines.append(line)
    if current_speaker is not None and current_lines:
        turns.append((current_speaker, "\n".join(current_lines).strip()))
    return [(s, msg) for s, msg in turns if msg]


def first_user_goal(turns):
    for speaker, msg in turns:
        if speaker.lower() in ("user", "you", "human"):
            first_line = msg.strip().splitlines()[0].strip()
            return (first_line[:180] + "...") if len(first_line) > 180 else first_line
    return "Not detected - edit this line in HANDOFF.md"


def build_handoff(turns, source_name: str, goal_override: str | None):
    goal = goal_override or first_user_goal(turns)
    today = date.today().isoformat()
    clean = "\n\n".join(f"**{s}:** {msg}" for s, msg in turns)

    return f"""# ContextHop Handoff
*Created {today} from `{source_name}` - {len(turns)} messages*

---

## 1. Paste this first in the NEW model

> You are continuing a conversation that started on another AI model.
> Read the context below carefully. Do NOT restart the task and do NOT
> re-ask questions that are already answered below.
> First reply with: (1) a 3-line summary of where we are, (2) what you
> think the next step is. Then wait for my instruction.

## 2. Context

**Original goal:** {goal}

**Where we left off:** [EDIT ME - 1 line: what was just done / what broke]

**Decisions already made:** [EDIT ME - or delete if none]

**Next step I want:** [EDIT ME - what the new model should do first]

## 3. Conversation so far

{clean}

---
*Made with ContextHop - https://github.com/aryancodes-dev/contexthop*
"""


def main():
    ap = argparse.ArgumentParser(description="Turn an AI chat transcript into a portable HANDOFF.md")
    ap.add_argument("input", help="Transcript file (.txt or .md)")
    ap.add_argument("-o", "--output", default="HANDOFF.md", help="Output file (default: HANDOFF.md)")
    ap.add_argument("--goal", default=None, help="Override the detected goal line")
    args = ap.parse_args()

    src = Path(args.input)
    if not src.exists():
        sys.exit(f"File not found: {src}")

    turns = parse_transcript(src.read_text(encoding="utf-8", errors="ignore"))
    if not turns:
        sys.exit("No messages found in that file.")

    out = Path(args.output)
    out.write_text(build_handoff(turns, src.name, args.goal), encoding="utf-8")
    print(f"Done: {len(turns)} messages -> {out} ({out.stat().st_size} bytes)")
    print("Next: open HANDOFF.md, fill the 3 [EDIT ME] lines, paste/upload it in the new model.")


if __name__ == "__main__":
    main()
