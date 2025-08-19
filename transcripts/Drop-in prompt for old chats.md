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

<%* if (files.trim()) { files.split(",").map(s=>s.trim()).filter(Boolean).forEach(f=> { tR += ` - ${f}\n`; }); } else { tR += " - \n" } %>

status: <%* tR += status %>

source: ChatGPT

permalink: <%* tR += permalink %>

---

  

## Transcript

  

> Paste the chat below this line. Keep raw Markdown from ChatGPT for fidelity
