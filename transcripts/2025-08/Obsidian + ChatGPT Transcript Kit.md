# Obsidian + ChatGPT Transcript Kit

This page gives you a **ready-to-use frontmatter template**, a **Templater snippet**, an optional **QuickAdd capture**, and a **drop-in prompt** you can paste into any old ChatGPT thread to export a clean Markdown transcript with standardized metadata.

---

## 1) Frontmatter schema (standardized)

```yaml
---
title: "${TP_TITLE}"
date: ${TP_DATE}
chat_id: ${TP_CHAT_ID}
participants: [Todd, GPT-5]
summary: "${TP_SUMMARY}"
keywords: [${TP_KEYWORDS}]
linked_repos: [${TP_LINKED_REPOS}]
files_created:
  - ${TP_FILES_CREATED}
status: ${TP_STATUS}
source: ChatGPT
permalink: ${TP_PERMALINK}
---
```

**Notes**

- Values with `${...}` are placeholders Templater/QuickAdd fills.
    
- `keywords` should be short, lower-case tokens (e.g., `obsidian, github, bundles`).
    
- `chat_id` can be any stable slug you choose (e.g., date + a short tag).
    

---

## 2) Obsidian Templater template (drop in `Templates/ChatGPT Transcript.md`)

The template will prompt you for key fields, then paste your transcript beneath the frontmatter.

```md
<%*
const now = tp.date.now("YYYY-MM-DD HH:mm");
const defTitle = `Chat Transcript - ${tp.date.now("YYYY-MM-DD")}`;
const title = await tp.system.prompt("Title", defTitle);
const chatId = await tp.system.prompt("Chat ID / slug", tp.date.now("YYYYMMDD-HHmm"));
const summary = await tp.system.prompt("One-line summary", "");
const keywords = await tp.system.prompt("Keywords (comma-separated)", "chatgpt, workflow");
const repos = await tp.system.prompt("Linked repos (comma-separated)", "");
const files = await tp.system.prompt("Files created (comma-separated)", "");
const status = await tp.system.prompt("Status", "complete");
const permalink = await tp.system.prompt("Source link (optional)", "");
_%>
---
title: "<%* tR += title %>"
date: <%* tR += now %>
chat_id: <%* tR += chatId %>
participants: [Todd, GPT-5]
summary: "<%* tR += summary %>"
keywords: [<%* tR += keywords.split(",").map(s=>s.trim()).filter(Boolean).join(", ") %>]
linked_repos: [<%* tR += repos.split(",").map(s=>s.trim()).filter(Boolean).join(", ") %>]
files_created:
<%* if (files.trim()) { files.split(",").map(s=>s.trim()).filter(Boolean).forEach(f=> { tR += `  - ${f}\n`; }); } else { tR += "  - \n" } %>
status: <%* tR += status %>
source: ChatGPT
permalink: <%* tR += permalink %>
---

## Transcript

> Paste the chat below this line. Keep raw Markdown from ChatGPT for fidelity.
```

**Usage**

- Create a new note using this template.
    
- Fill prompts, then paste the transcript.
    
- Save; Obsidian Git plugin can auto-commit on save.
    

---

## 3) QuickAdd capture (optional)

If you use the **QuickAdd** plugin, configure a capture that:

- **File name:** `chatgpt/<% tp.date.now("YYYY/MM/YYYY-MM-DD-HHmm") %> - <%* tR += title %>.md`
    
- **Template:** the Templater file above
    
- **Variables:** QuickAdd will pass variables if desired, but the Templater prompts already handle it.
    

Minimal QuickAdd JSON (paste into QuickAdd settings → _Import from JSON_):

```json
{
  "choices": [
    {
      "name": "New ChatGPT Transcript",
      "type": "Macro",
      "macro": [
        {
          "name": "Templater",
          "type": "Templater",
          "templatePath": "Templates/ChatGPT Transcript.md"
        }
      ],
      "hotkey": "Ctrl+Alt+G"
    }
  ]
}
```

---

## 4) Drop-in prompt for **old chats** (paste this at the end of any ChatGPT thread)

This produces a **single Markdown file** with filled frontmatter and a clean transcript. After the model returns it, copy the whole thing into Obsidian.

```
You are a Markdown export assistant. Read this entire chat and produce a single .md document with:

1) A YAML frontmatter block:
- title: A concise title based on the main purpose of the chat
- date: The chat’s start time (if unknown, use today’s date in YYYY-MM-DD HH:mm, America/Chicago)
- chat_id: A stable slug (YYYYMMDD-HHmm plus a short topic)
- participants: [Todd, GPT-5]
- summary: One concise sentence summarizing decisions/outputs
- keywords: 5–10 short tags in lowercase
- linked_repos: repo names explicitly mentioned (or empty)
- files_created: list any filenames that were drafted/created in the chat
- status: complete
- source: ChatGPT
- permalink: leave blank unless an explicit chat link is available

2) A `## Transcript` section containing the full conversation in readable Markdown. Prefix each line with **User:** or **Assistant:** and keep code blocks intact. Do not add commentary or hallucinate content.

Output only the final Markdown document.
```

> Tip: If the chat is massive, ask the assistant to export in **parts** (e.g., “export part 1/3, then 2/3, 3/3”). Paste each part consecutively under `## Transcript`.

---

## 5) Filename pattern and folders

- Suggested folder: `chatgpt/2025/08/`
    
- Filename: `YYYY-MM-DD-HHmm - <slug>.md` (e.g., `2025-08-18-1840 - obsidian-export-kit.md`)
    

---

## 6) Optional: thin PowerShell wrapper (Windows)

Watches your clipboard; when you copy Markdown, it saves to your vault with time-stamped filename and opens it in Obsidian.

```powershell
# Save as Save-GPTClipboard.ps1 and run in a terminal inside your vault root
Add-Type -AssemblyName PresentationCore

$fs = "chatgpt/$(Get-Date -Format 'yyyy/MM')"
New-Item -ItemType Directory -Force -Path $fs | Out-Null

while ($true) {
  Start-Sleep -Milliseconds 800
  if ([Windows.Clipboard]::ContainsText()) {
    $md = [Windows.Clipboard]::GetText()
    if ($md.Length -gt 100) {
      $name = (Get-Date -Format 'yyyy-MM-dd-HHmm') + " - pasted.md"
      $path = Join-Path $fs $name
      $md | Out-File -FilePath $path -Encoding UTF8
      Write-Host "Saved: $path"
      [Windows.Clipboard]::Clear()
      Start-Process "obsidian://open?path=$([Uri]::EscapeDataString((Resolve-Path $path).Path))"
    }
  }
}
```

---

## 7) Tagging conventions (optional but helpful)

- **Process tags:** `#chatgpt`, `#transcript`, `#bundle`, `#script`, `#decision`
    
- **Domain tags:** `#obsidian`, `#github`, `#python`, `#accounting`, `#cmastudy`
    
- **Status tags:** `#todo`, `#draft`, `#complete`
    

---

## 8) Validation checklist

- Frontmatter present and valid YAML
    
- Transcript complete (all code blocks preserved)
    
- Links to repos/files captured
    
- Summary is one sentence and specific
    
- Filename and folder follow the pattern
    

Happy archiving. Paste, commit, and your vault becomes a searchable memory palace. 🚀