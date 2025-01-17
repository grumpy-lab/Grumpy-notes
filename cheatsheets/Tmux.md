#cheatsheets #Tmuix

## Commands

### Session

```bash
# Start a new tmux session.
tmux

# Start a new tmux session with name.
tmux new -s <session-name>

# List all sessions.
tmux ls

# Attach to the last session.
tmux attach

# Attach to a session with name.
tmux attach -t <session-name>

# Kill a session.
tmux kill-session -t <session-name>

# Kill sessions other than the current one.
tmux kill-session -a

# Kill sessions other than the named one.
tmux kill-session -a -t <session-name>
```

### Window

```bash
# Create a new window and switch to it.
tmux new-window

# Create a a new window with name, but do not swith to it.
tmux new-window -t -n <window-name>

# Kill the current window.
tmux kill-window

# Kill the target window.
tmux kill-window -t <window-name>

# Send keys to the target window. (End with C-j for enter)
tmux send-keys -t <window-name> <command> C-j
```

### Info

```bash
# Show tmux session information.
tmux info
```

### Config

```bash
# Reload config.
tmux source-file ~/.tmux.conf

# Show config.
tmux show-options -g
```

## HotKeys

### Session Management

|   |   |
|---|---|
|`C-b d`|Dettach from session|
|`C-b s`|Show all sessions|
|`C-b $`|Rename sessions|
|`C-b (`|Go to the previous session|
|`C-b )`|Go to the next session|

### Window Management

|   |   |
|---|---|
|`C-b c`|Create a new window|
|`C-b p`|Go to the previous window|
|`C-b n`|Go to the next window|
|`C-b ,`|Rename window|
|`C-b &`|Close window|
|`C-b w`|List window|
|`C-b f`|Find window|
|`C-b l`|Last window|
|`C-b .`|Move window|
|`C-b 0...9`|Goto # window|

### Pane Management

|   |   |
|---|---|
|`C-b "`|Split horizontally|
|`C-b %`|Split vertically|
|`C-b !`|Convert pane to window|
|`C-b x`|Kill pane|
|`C-b <arrow>`|Switch panes|
|`C-b C-<arrow>`|Adjust pane size|
|`C-b <space>`|Toggle pane layout|
|`C-b {/}`|Move to Left/Right|
|`C-b o`|Goto next panes|
|`C-b z`|toggle full-screen|
|`C-b ;`|Toggle Last pane|
|`C-b q`|Show numbers|
|`C-b q 0...9`|Goto # pane|