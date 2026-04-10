# session-record

Record terminal sessions using macOS `script`. Defaults to readable output capture for commands, output, SSH/telnet sessions, tmux, and interactive programs.

## Install

```bash
ln -s "$(pwd)/session-record" ~/.local/bin/session-record
```

## Usage

```bash
session-record start [name]     # Start recording (name defaults to timestamp)
session-record stop             # Show how to stop the current recording
session-record list             # List all recorded sessions
session-record stream <name>    # Stream a session live from the log
session-record attach [name]    # Attach read-only to the active/live session
session-record show <name>      # Show a session with ANSI codes stripped
session-record raw <name>       # Show raw session recording
session-record replay <name>    # Replay a session
session-record delete <name>    # Delete a session
session-record clean [days]     # Delete sessions older than N days (default 30)
```

To stop a recording, type `exit` or press `Ctrl-D` in the recorded shell.

`attach` is read-only. It follows the live session output from another terminal, but it does not re-enter the same interactive shell.

Logs are stored in `~/.session-logs/`.

## Keystroke capture

By default, `session-record start` records terminal output only. This keeps
`session-record show` readable for interactive shells such as SSH, telnet, and
paged device CLIs.

If you need raw keystroke capture for forensic debugging, enable it explicitly:

```bash
SESSION_RECORD_CAPTURE_KEYS=1 session-record start [name]
```

Raw keystroke capture uses `script -k`, which can make cleaned transcripts look
jumbled because cursor edits, backspaces, and prompt redraws are flattened when
ANSI control sequences are stripped.

## What it captures

- Command output and remote CLI echoes (stdout + stderr)
- Optional raw local keystroke capture with `SESSION_RECORD_CAPTURE_KEYS=1`
- SSH and telnet session content (both directions)
- Interactive programs (vim, top, etc.)
- tmux pane output (when tmux runs inside the recorded session)
- Prompts, error messages, log streams
