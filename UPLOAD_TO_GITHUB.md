# Upload ContextHop to GitHub — Step by Step
For: Aryan Kumar Shah (github.com/aryancodes-dev) | Repo name: contexthop
Time needed: ~10 minutes on PC, ~20 minutes on phone only.

---

## STEP 1 — Create the empty repo (do this first, on phone or PC)

1. Open https://github.com and sign in as **aryancodes-dev**
2. Top-right **+** → **New repository**  (or open https://github.com/new)
3. Fill exactly this:

   - **Repository name:** `contexthop`
   - **Description** (copy-paste):
     ```
     Carry an AI chat to any other model without starting over — portable HANDOFF.md generator for ChatGPT, Claude & Gemini. No API key, no server.
     ```
   - **Public** ✓ (must be Public for open source + portfolio)
   - **DO NOT tick** "Add a README file"
   - **DO NOT add** .gitignore or License — we already have both in the kit
4. Click **Create repository**
5. Leave that page open — you will need its URL:
   `https://github.com/aryancodes-dev/contexthop.git`

> If GitHub says the name is taken on your account, it means you already
> created it — open it and go straight to Step 2.

---

## STEP 2A — Upload from PC / Laptop with Git (BEST way)

You need the `context-hop-starter.zip` file on the PC. Unzip it.
You will get a folder named `context-hop`. Rename it to `contexthop`.

Open Terminal / Git Bash **inside** that folder and paste, line by line:

```bash
git init
git add .
git commit -m "v0.1: ContextHop - Python CLI + Magic Handoff Prompt"
git branch -M main
git remote add origin https://github.com/aryancodes-dev/contexthop.git
git push -u origin main
```

**If it asks for login:** username = `aryancodes-dev`, password =
a Personal Access Token, NOT your GitHub password.
Create one: GitHub → Settings → Developer settings → Personal access
tokens → Tokens (classic) → Generate new token → tick `repo` → Generate.
Paste the token as the password. (Save it somewhere private.)

**Easier alternative — GitHub Desktop:** File → Add Local Repository →
choose the `contexthop` folder → "Publish repository". No commands.

### If push is rejected ("rejected / fetch first")
It means you accidentally ticked "Add a README". Run:
```bash
git pull origin main --allow-unrelated-histories
git push -u origin main
```

---

## STEP 2B — Upload from PHONE only (no PC)

GitHub's phone web upload cannot upload folders, so create folders
using the `/` trick in the file name:

1. Open your new repo in Chrome (not the GitHub app — use
   **Desktop site** in Chrome ⋮ menu, GitHub upload works better there)
2. **Add file → Upload files** → upload these 4 root files from the kit:
   `README.md`, `context_hop.py`, `LICENSE`, `.gitignore`
   (Note: some phone file pickers hide `.gitignore` — skip it on phone
   if you can't see it, it is not critical.)
   Write commit message: `v0.1: ContextHop - Python CLI + Magic Handoff Prompt`
   → **Commit changes**
3. **Add file → Create new file** → in the name box type exactly:
   `prompts/magic_handoff_prompt.md`
   GitHub auto-creates the `prompts` folder. Paste the file's content
   (open it from the kit and copy all) → **Commit changes**
4. Repeat **Create new file** for:
   - `examples/sample_chat.txt` — paste its content → Commit
   - `examples/sample_HANDOFF.md` — paste its content → Commit

Phone uploads are slower — if you have ANY access to a PC/laptop,
Step 2A is much better.

---

## STEP 3 — Verify (2 minutes)

Open https://github.com/aryancodes-dev/contexthop and check:
- [ ] README is shown nicely on the repo home page (not raw code)
- [ ] You can see: `context_hop.py`, `prompts/`, `examples/`, `LICENSE`
- [ ] Clicking `context_hop.py` shows the Python code

If yes — **you are live.** Send this link to anyone.

---

## STEP 4 — Make it discoverable (5 minutes, important)

On the repo page, click the ⚙️ gear next to **About** (right side):
- **Description:** (same as Step 1)
- **Website:** `https://aryancodes-dev.github.io/`
- **Topics** (add one by one):
  ```
  ai  chatgpt  claude  gemini  llm  python  open-source  productivity  context  developer-tools
  ```
- Save

Then pin it to your profile: your profile page → **Customize your pins**
→ tick **contexthop**. This helps your searchable-identity goal.

---

## STEP 5 — Create your first Release (makes it look real)

1. Repo page → right side **Releases → Create a new release**
2. **Tag:** `v0.1.0` → Create new tag
3. **Title:** `v0.1.0 — First release`
4. **Notes** (copy-paste):
   ```
   First public release of ContextHop.

   - Python CLI: turn a ChatGPT / Claude / Gemini transcript into a portable HANDOFF.md
   - Magic Handoff Prompt: no-install method that works on any model, even on mobile
   - Example chat + generated handoff included
   - No API key, no server, 100% local. MIT License.
   ```
5. **Publish release**

---

## After upload — tell Muse: "uploaded"
Then we will: verify your live repo link together, add ContextHop as
Project #1 on your portfolio website and resume, and plan v0.2
(auto-detect ChatGPT / Claude JSON exports).
