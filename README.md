# 🖥️ tmux Cheat Sheet

> A clean, complete reference for terminal multiplexing with tmux.

---

## 🔑 Prefix Key

All tmux shortcuts are triggered by pressing the **prefix key** first.

| Default Prefix | Keys |
|---|---|
| `Ctrl + b` | Press together, release, then press shortcut |

> **Example:** `Ctrl+b` → `c` creates a new window.

---

## 📁 Session Management

```bash
tmux                        # Start a new session
tmux new -s mysession       # Start a named session
tmux ls                     # List all sessions
tmux attach -t mysession    # Attach to a named session
tmux attach                 # Attach to the last session
tmux kill-session -t name   # Kill a named session
tmux kill-server            # Kill all sessions and the server
```

| Shortcut | Action |
|---|---|
| `Prefix + $` | Rename current session |
| `Prefix + s` | List & switch sessions interactively |
| `Prefix + d` | Detach from current session |
| `Prefix + (` | Switch to previous session |
| `Prefix + )` | Switch to next session |

---

## 🪟 Window Management

```bash
# Windows are like tabs inside a session
```

| Shortcut | Action |
|---|---|
| `Prefix + c` | Create a new window |
| `Prefix + ,` | Rename current window |
| `Prefix + &` | Kill current window |
| `Prefix + n` | Switch to next window |
| `Prefix + p` | Switch to previous window |
| `Prefix + 0–9` | Switch to window by number |
| `Prefix + w` | List & switch windows interactively |
| `Prefix + l` | Switch to last (previously used) window |

---

## 🔲 Pane Management

```bash
# Panes split the current window into multiple terminals
```

| Shortcut | Action |
|---|---|
| `Prefix + %` | Split pane **vertically** (left/right) |
| `Prefix + "` | Split pane **horizontally** (top/bottom) |
| `Prefix + x` | Close current pane |
| `Prefix + z` | **Zoom** / unzoom current pane (toggle fullscreen) |
| `Prefix + {` | Move pane left |
| `Prefix + }` | Move pane right |
| `Prefix + q` | Show pane numbers (press number to jump) |
| `Prefix + !` | Break pane into its own window |

### 🔀 Switch Between Panes

| Shortcut | Action |
|---|---|
| `Prefix + Arrow Key` | Move to pane in that direction |
| `Prefix + o` | Cycle through panes |
| `Prefix + ;` | Switch to last active pane |

### ↔️ Resize Panes

| Shortcut | Action |
|---|---|
| `Prefix + Ctrl + Arrow` | Resize pane in that direction |
| `Prefix + Alt + Arrow` | Resize pane in larger steps |

---

## 🧭 Navigation Shortcuts

| Shortcut | Action |
|---|---|
| `Prefix + [` | Enter scroll / copy mode |
| `Prefix + ?` | Show all key bindings |
| `Prefix + t` | Show a clock in current pane |
| `Prefix + ~` | Show tmux messages log |
| `q` | Exit pane number display |

---

## 📋 Copy Mode

```bash
Prefix + [          # Enter copy mode (scroll with arrow keys or Page Up/Down)
```

| Key (in copy mode) | Action |
|---|---|
| `Space` | Start selection |
| `Enter` | Copy selection & exit copy mode |
| `Prefix + ]` | Paste copied text |
| `q` | Quit copy mode without copying |
| `g` | Go to top of buffer |
| `G` | Go to bottom of buffer |
| `/` | Search forward |
| `?` | Search backward |

> 💡 **Tip:** Add `set-window-option -g mode-keys vi` to `~/.tmux.conf` to use **vi-style** keys in copy mode.

---

## 🗂️ Layout Controls

```bash
Prefix + Space      # Cycle through preset layouts
```

| Layout | Description |
|---|---|
| `even-horizontal` | Panes side by side, equal width |
| `even-vertical` | Panes stacked, equal height |
| `main-horizontal` | One large pane on top, rest below |
| `main-vertical` | One large pane on left, rest on right |
| `tiled` | Grid layout |

```bash
tmux select-layout tiled    # Apply layout from command line
```

---

## ⚙️ Config File

tmux reads its config from `~/.tmux.conf` on startup.

```bash
touch ~/.tmux.conf           # Create config file if it doesn't exist
```

```bash
# Reload config without restarting tmux
Prefix + :source-file ~/.tmux.conf

# Or from shell:
tmux source-file ~/.tmux.conf
```

### 📝 Sample `~/.tmux.conf`

```bash
# Change prefix to Ctrl+a (like GNU Screen)
unbind C-b
set-prefix C-a
bind C-a send-prefix

# Enable mouse support
set -g mouse on

# Start window/pane numbering from 1
set -g base-index 1
setw -g pane-base-index 1

# Vi keys in copy mode
setw -g mode-keys vi

# Increase scrollback buffer
set -g history-limit 10000

# Status bar styling
set -g status-bg colour235
set -g status-fg colour136
```

---

## 🛠️ Customization

### Change the Prefix Key

```bash
# In ~/.tmux.conf — replace Ctrl+b with Ctrl+a
unbind C-b
set-option -g prefix C-a
bind-key C-a send-prefix
```

### Custom Split Shortcuts

```bash
# Use | and - for splits (more intuitive)
bind | split-window -h
bind - split-window -v
unbind '"'
unbind %
```

---

## 🌐 Useful Tips

### SSH & Remote Workflows

```bash
tmux new -s work            # Start a named session before SSH work
# If SSH disconnects, your session stays alive on the server
tmux attach -t work         # Re-attach after reconnecting
```

### Nested tmux (Local + Remote)

```bash
# Press prefix twice to send prefix to the inner (remote) tmux
Ctrl+b  Ctrl+b              # e.g., send Ctrl+b to remote session
```

### Scripted Session Setup

```bash
# Start a dev environment in one command
tmux new-session -d -s dev -n editor
tmux send-keys -t dev 'nvim .' Enter
tmux split-window -h -t dev
tmux send-keys -t dev 'npm run dev' Enter
tmux attach -t dev
```

### General Tips

- **Always name your sessions** — makes re-attaching fast and clear.
- Use `tmux ls` before attaching to avoid accidental duplicate sessions.
- Combine tmux with `ssh-agent` for persistent SSH keys across reconnects.
- Use a status bar plugin like **tmux-powerline** or **catppuccin-tmux** for a polished look.

---

## 🚪 Exit Commands

```bash
exit                        # Close current pane/window (from shell)
Prefix + x                  # Kill pane (with confirmation)
Prefix + &                  # Kill window (with confirmation)
tmux kill-session           # Kill current session
tmux kill-server            # Kill everything
```

---

## 📌 Quick Reference Card

| Action | Command/Shortcut |
|---|---|
| New session | `tmux new -s name` |
| Attach session | `tmux attach -t name` |
| Detach | `Prefix + d` |
| New window | `Prefix + c` |
| Split vertical | `Prefix + %` |
| Split horizontal | `Prefix + "` |
| Zoom pane | `Prefix + z` |
| Copy mode | `Prefix + [` |
| Paste | `Prefix + ]` |
| Reload config | `Prefix + :source-file ~/.tmux.conf` |
| Show keybindings | `Prefix + ?` |

---

*Generated for tmux 3.x · Compatible with most Unix/Linux/macOS systems*
