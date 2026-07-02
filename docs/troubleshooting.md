# Troubleshooting

## "This conversation is too long to continue"

**Cause:** Too many MCP connectors are enabled for the Claude Code session. Each
connector injects its entire tool catalog into the context window before any
work begins, exhausting the available space.

**Fix:**
1. Claude Code UI → **Settings → Connectors**.
2. Disable connectors you don't need (keep **GitHub** for this repo).
3. Start a **new chat** (changes only apply to fresh sessions).

See [`../CLAUDE.md`](../CLAUDE.md) for details.

---

## A `C:\WINDOWS\SYSTEM32\cmd.exe` window keeps popping up (Windows)

> Note: this is a local Windows issue, **not** something the cloud coding
> environment can inspect or fix. Steps below are for the affected PC.

`cmd.exe` is a normal, legitimate Windows file — the real question is *what
keeps launching it*. Usually it's a scheduled task or startup entry; occasionally
it's unwanted software.

**1. Find what launches it**
- Open **Task Scheduler** (Start → type "Task Scheduler") → **Task Scheduler
  Library**. Look for tasks with random names or that run every few minutes
  (matching the pop-up frequency). Click a suspect → **Actions** tab shows the
  exact program/script it runs.
- Open **Task Manager** (Ctrl+Shift+Esc) → **Startup apps** tab; note anything
  unfamiliar.
- Run `shell:startup` (Win+R) to see per-user startup items.

**2. Scan for malware**
- Start → **Windows Security** → **Virus & threat protection** → **Scan
  options** → **Full scan** → **Scan now**. Follow removal prompts.

**3. Do not**
- Delete files in `System32` (including `cmd.exe` itself) — that breaks Windows.
- Install random "PC cleaner" tools from ads — these are often the cause.

**4. Disable the culprit**
- Once identified in Task Scheduler, right-click the task → **Disable** (don't
  delete until you're sure). Then confirm the pop-ups stop.
