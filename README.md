# session-record

Record terminal sessions using macOS `script`. Captures everything — commands, output, SSH/telnet sessions, tmux, interactive programs.

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

## What it captures

- All command input and output (stdout + stderr)
- SSH and telnet session content (both directions)
- Interactive programs (vim, top, etc.)
- tmux pane output (when tmux runs inside the recorded session)
- Prompts, error messages, log streams
