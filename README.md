<p align="center">
  <img src="logo.png" alt="Fugu Studio — Sakana AI" width="520">
</p>

<h1 align="center">Fugu Studio</h1>

<p align="center">
  A clean desktop client for the <b>Sakana Fugu / Fugu Ultra</b> Responses API —
  chat, attach files, and let Fugu read &amp; edit a whole project folder for you.
</p>

---

## ✨ Features

- **Multi-tab chat** — each tab is its own conversation with its own memory.
- **Bring your own files** — attach images, PDF, DOCX, PPTX, code, and text; drag-and-drop or paste images straight in.
- **Workspace folder mode** 📂 — point Fugu at a project/study folder and it reads every file in it (recursively, with smart ignores for `.git`, `node_modules`, etc.).
- **Live edits** — Fugu can create, modify, and delete files in that folder. Changes are applied automatically.
- **Activity log + one-click revert** 📜 — every file change gets an ID and is fully recoverable.
- **Markdown + code rendering** with copy buttons, **light/dark themes**, token-usage tracking, and saved chats.

---

## 🔑 Get your API key (required)

Fugu Studio does **not** ship with a key — you use your own.

1. Go to **<https://console.sakana.ai/api-keys>**
2. Sign in and create a new API key.
3. Copy it. You'll paste it into the app on first launch (next section).

> Your key stays **only on your machine** — see [Where your key is stored](#-where-your-key-is-stored).

---

## 🚀 Quick start

### 1. Install Python
Python **3.9+** (3.11 recommended). On Windows, tick *"Add Python to PATH"* during install.

### 2. Install dependencies
```bash
pip install -r requirements.txt
```
<sub>Only <code>openai</code> is strictly required; the rest unlock PDF/DOCX/PPTX/image support and drag-and-drop.</sub>

### 3. Run
```bash
python fugu.py
```
…or just double-click `fugu.py`.

### 4. Add your key
Paste the key from the console into the **API key** box at the top and click **Save key**. The dot turns green and you're ready. You only do this once.

---

## 💬 How to use

### Plain chat
1. Pick a **Model** (`fugu` or `fugu-ultra`) and optional **Reasoning** (`high` / `xhigh`).
2. Type a message and press **Enter** (or click **Send**). Use **Shift+Enter** for a newline.
3. Attach files with **Add files…**, drag-and-drop, or paste an image with **Ctrl+V**.

### Workspace folder mode (coding / studying)
1. Click **📁 Folder → Browse Folder…** and pick your project or study folder.
2. The left **Workspace** panel lists every recognised file (double-click to open one). Junk folders like `.git`, `node_modules`, `__pycache__`, `venv`, build/cache dirs are skipped automatically.
3. Just ask — Fugu sees the current contents of all those files. Examples:
   - *"Explain what `main.py` does and find any bugs."*
   - *"Combine `a.txt` and `b.txt` into `notes.txt`, then delete the originals."*
   - *"Add input validation to the signup form."*
4. When Fugu changes files, the edits are **applied to disk automatically** and you'll see a note like:
   `✓ Applied 2 change(s): ✎main.py [#3], 🗑old.py [#4]`

> **"Send folder with messages"** checkbox: leave on to keep Fugu in sync with your files. Turn it off (or click **Clear**) to stop sending the folder and save tokens.

### Activity log & undo
Click **📜 Activity log** to see every change Fugu made — with an **ID**, timestamp, action, file, and a diff. Select any entry and hit **↩ Revert selected** to restore the file to how it was before that change (reverting a deletion re-creates the file). Nothing is ever lost.

---

## 📁 What can be attached / read

| Input            | How Fugu receives it                                   |
|------------------|--------------------------------------------------------|
| Images           | Sent natively (auto-downscaled if very large)          |
| PDF              | Text extracted; scanned pages auto-rendered to images  |
| DOCX             | Text extracted (paragraphs + tables)                   |
| PPTX             | Text extracted (all slides)                            |
| XLSX / XLSM      | Text extracted (all sheets)                            |
| Code / TXT / MD / CSV / JSON / … | Sent as text                           |
| **Any other file** | Read as text if it's text-like; otherwise sent as a name/type/size placeholder |

<sub>You can attach, browse, or scan **any file type**. Fugu's API natively accepts text and images only, so documents are read locally and their text/visuals are passed in; truly binary files (zip, audio, executables, …) are represented by their metadata.</sub>

---

## 🔒 Where your key is stored

- The app saves your key to a local file named **`api_key.txt`** in this folder, used only to talk to Sakana's API.
- **`api_key.txt` is git-ignored**, so it is never committed or pushed. The same goes for your `chats/`, `usage_stats.json`, and workspace history.
- Prefer an environment variable? Set **`FUGU_API_KEY`** (and optionally `FUGU_BASE_URL`, default `https://api.sakana.ai`) and skip the in-app box.

> 🚫 **Never** paste your key into the code or commit `api_key.txt`. Treat it like a password.

---

## 🛠 Troubleshooting

- **"No API key"** → paste your key in the box and click **Save key**, or set `FUGU_API_KEY`.
- **Drag-and-drop doesn't work** → `pip install tkinterdnd2` (it's optional).
- **PDF/DOCX/PPTX won't read** → install the file deps: `pip install -r requirements.txt`.

---

<p align="center"><sub>© 2026 Md. Sabbir Ahmed · Fugu Studio · Built on Sakana AI</sub></p>
