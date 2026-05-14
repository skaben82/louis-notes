# Notes System — Claude Instructions

This folder is Louis's personal notes system. It replaces Notion for day-to-day note capture and organisation. These instructions tell Claude exactly how to handle everything in this folder.

---

## Folder Location

The notes folder lives in iCloud Drive so it syncs across all of Louis's devices:

**Mac path:** `~/Library/Mobile Documents/com~apple~CloudDocs/notes/`

All note files, subfolders, and the dashboard (index.html) must be saved to this path. Never save notes to the old Claude Main Folder path.

---

## Who Louis Is

Louis Ebanks is a Chartered Accountant (FCCA) and finance transformation coach. He works with manufacturing and engineering SMEs. He's also building a content creation presence and a side hustle. He is non-technical — plain English always.

---

## Folder Structure

```
/notes/
  CLAUDE.md           ← this file
  index.html          ← master dashboard (always keep updated)
  inbox.txt           ← universal capture file — notes added from any device land here
  /work/              ← client notes, meeting notes, coaching work
  /personal/          ← personal life, family, health, interests
  /content/           ← content ideas, drafts, social media, YouTube
  /side-hustle/       ← side hustle experiments, research, revenue tracking
```

---

## How Louis Adds Notes

Louis will either:
1. Type a note directly into this session
2. Paste a raw voice recording transcript

In both cases, he will tell Claude:
- What the note is about
- Which area it belongs to (work / personal / content / side-hustle)
- Any actions with dates (if he knows them — Claude should also detect these automatically)

---

## What Claude Does With a Note

### Step 1 — Clean and structure the content
- If it's a voice transcript: remove filler words (um, uh, like, you know), fix grammar, break into clear paragraphs. Preserve the meaning exactly — do not paraphrase or summarise unless asked.
- If it's typed: light editing only. Fix obvious typos. Don't rewrite.
- Use British English throughout.

### Step 2 — Detect actions and dates
Scan the note for anything that sounds like an action or a commitment:
- Phrases like "I need to", "follow up", "call", "send", "book", "remind me", "by [date]", "before [date]", "next week", "tomorrow"
- Extract these as a clean list of action items, each with a date if one is mentioned or implied
- If no date is given for an action, flag it as "No date set"

### Step 3 — Create the HTML note file
Save the note as an HTML file in the correct subfolder. File naming: `YYYY-MM-DD-short-title.html` (e.g. `2026-05-10-mcbraida-meeting.html`)

Use the HTML note template below.

### Step 4 — Create Google Calendar events for dated actions
For any action that has a specific date, create a Google Calendar event:
- Title: the action item text
- Date: the date mentioned in the note
- Description: "From note: [note title] — [link to note file if possible]"
- Calendar: Louis's primary Google Calendar

### Step 5 — Update the dashboard
After saving the note, update `index.html` to include the new note. The dashboard must always reflect the current state of all notes.

---

## HTML Note Template

Every note is saved as a self-contained HTML file using this structure:

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>[Note Title] — [Date]</title>
  <style>
    /* Clean minimal style — slate blue accents, white background */
    body { font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', sans-serif; max-width: 800px; margin: 40px auto; padding: 0 24px; color: #1a1a1a; background: #fff; line-height: 1.7; }
    header { border-bottom: 2px solid #3b5bdb; padding-bottom: 16px; margin-bottom: 28px; }
    h1 { font-size: 1.6rem; margin: 0 0 8px; color: #1a1a1a; }
    .meta { font-size: 0.85rem; color: #666; display: flex; gap: 16px; flex-wrap: wrap; }
    .tag { background: #e8eeff; color: #3b5bdb; padding: 2px 10px; border-radius: 20px; font-size: 0.78rem; font-weight: 600; text-transform: uppercase; letter-spacing: 0.04em; }
    .tag.work { background: #e8eeff; color: #3b5bdb; }
    .tag.personal { background: #e8f5e9; color: #2e7d32; }
    .tag.content { background: #fff3e0; color: #e65100; }
    .tag.side-hustle { background: #fce4ec; color: #c62828; }
    .note-body { margin-bottom: 32px; }
    .note-body p { margin: 0 0 16px; }
    .actions { background: #f8f9ff; border-left: 4px solid #3b5bdb; border-radius: 0 8px 8px 0; padding: 20px 24px; margin-top: 32px; }
    .actions h2 { font-size: 1rem; margin: 0 0 14px; color: #3b5bdb; text-transform: uppercase; letter-spacing: 0.06em; font-size: 0.8rem; }
    .action-item { display: flex; justify-content: space-between; align-items: flex-start; padding: 10px 0; border-bottom: 1px solid #e0e4f0; gap: 16px; }
    .action-item:last-child { border-bottom: none; }
    .action-text { flex: 1; font-size: 0.95rem; }
    .action-date { font-size: 0.82rem; color: #fff; background: #3b5bdb; padding: 2px 10px; border-radius: 20px; white-space: nowrap; }
    .action-date.no-date { background: #aaa; }
    .action-date.overdue { background: #c62828; }
    .back-link { display: inline-block; margin-top: 32px; font-size: 0.85rem; color: #3b5bdb; text-decoration: none; }
    .back-link:hover { text-decoration: underline; }
  </style>
</head>
<body>
  <header>
    <h1>[Note Title]</h1>
    <div class="meta">
      <span>[Date — DD Month YYYY]</span>
      <span class="tag [area]">[Area]</span>
    </div>
  </header>

  <div class="note-body">
    [Note content goes here — cleaned and formatted into paragraphs]
  </div>

  [If there are actions:]
  <div class="actions">
    <h2>Actions</h2>
    <div class="action-item">
      <span class="action-text">[Action description]</span>
      <span class="action-date">[Date or "No date set"]</span>
    </div>
  </div>

  <a href="../index.html" class="back-link">← Back to dashboard</a>
</body>
</html>
```

---

## Dashboard (index.html)

The dashboard must:
- List all notes across all areas
- Show note title, date, area tag, and a snippet of the first sentence
- Have a search bar (searches title and content)
- Have filter buttons by area (All / Work / Personal / Content / Side Hustle)
- Have an "Actions" panel at the top flagging any note with outstanding actions — sorted by due date, overdue items highlighted in red
- Update automatically whenever a new note is added

---

## Tone and Language

- British English throughout
- Plain, functional language in note summaries
- Do not add opinions, commentary, or suggestions to notes unless asked
- The system is invisible — Louis should barely notice it. Notes go in messy, come out clean.

---

## Calendar Integration

When an action with a date is detected:
- Use the connected Google Calendar MCP to create an event
- Keep event titles short and action-focused (e.g. "Follow up with McBraida re: invoice")
- Always confirm with Louis before creating calendar events — list what you're about to create and ask for a quick yes/no before doing it

---

## Processing the Inbox

When Louis says "process my inbox" (or similar), Claude must:

### Step 1 — Read inbox.txt
Read the full contents of `inbox.txt`. Parse each entry between `---` dividers. Each entry has:
- `DATE:` — the date the note was taken (use this as the note date, not today's date)
- `AREA:` — which folder it belongs in (work / personal / content / side-hustle)
- `NOTE:` — the raw content

### Step 2 — Confirm before filing
List all entries found — title (Claude's best guess at a short title), date, and area — and ask Louis to confirm or correct before doing anything. Example:

> "Found 3 notes in your inbox:
> 1. McBraida Q2 update — 10 May — Work ✓
> 2. YouTube episode idea — 9 May — Content ✓
> 3. Car service reminder — 8 May — Personal ✓ (or Personal?)
> Happy for me to file these?"

### Step 3 — Process each note
For each confirmed entry, follow the standard note process:
- Clean and structure the content (Steps 1–5 from "What Claude Does With a Note" above)
- Create the HTML file in the correct subfolder
- Detect actions and dates
- Propose any calendar events for Louis's approval
- Update the dashboard

### Step 4 — Clear the inbox
Once all notes are processed and confirmed, remove the processed entries from inbox.txt, leaving only the header/instructions section intact. The file should be ready for the next batch of notes.

### If an entry is ambiguous
If the AREA is missing or unclear, ask Louis before filing — don't guess.
If the DATE is missing, use today's date and flag it to Louis.

---

## How Louis Adds Notes From Other Devices

Louis uses `inbox.txt` as a universal capture point across all his devices. The file is stored in Google Drive so it's accessible everywhere. He adds notes in this format:

```
---
DATE: DD Month YYYY
AREA: work / personal / content / side-hustle
NOTE:
[content here]
```

He doesn't need to format or tidy anything. Just the date, area, and raw content. Claude handles the rest when he says "process my inbox".

---

## Model

Always use the Haiku model for inbox processing and note filing. The task is straightforward — no higher model is needed.

---

## Rules

- Never delete a note without explicit confirmation
- Never send emails or publish anything
- Never rewrite the substance of a note — only clean the presentation
- If a note is ambiguous about which area it belongs to, ask before filing it
- Always update index.html after adding a note
- Do not ask for approval before filing notes — process and file everything automatically. Only pause if an area is missing or genuinely unclear.
