# 🧠 tmux Cheat Sheet

> Terminal multiplexer: manage multiple sessions, windows, and panes in one terminal.

---

## 🚀 Start & Sessions

tmux                    # start new session
tmux new -s name        # create session with name
tmux new -s name -d     # create session in background (detached)
tmux ls                 # list sessions
tmux attach -t name     # attach to session
tmux kill-session -t name  # kill session
tmux kill-server        # kill all sessions

---

## ⌨️ Prefix Key

Default prefix:
Ctrl + B

All shortcuts below are used after pressing prefix.

---

## 🔌 Detach & Help

d        # detach from session
?        # list all key bindings
:        # enter command mode

---

## 🪟 Windows (Tabs)

c        # create new window
n        # next window
p        # previous window
w        # list windows
,        # rename window
&        # kill window
0-9      # switch to window number

---

## 📐 Panes (Splits)

%        # vertical split
"        # horizontal split
o        # switch pane
x        # kill pane
z        # toggle zoom

---

## 🔄 Pane Navigation

Arrow Keys   # move between panes
q            # show pane numbers

---

## 📏 Resize Panes

Ctrl + B + Arrow Keys   # resize pane (hold Ctrl)

---

## 🔀 Layouts

Space      # cycle layouts
Alt + 1-5  # select layout (if supported)

---

## 📋 Copy Mode

[        # enter copy mode
Space    # start selection
Enter    # copy selection
]        # paste

---

## 🔁 Rename & Info

$        # rename session
i        # show info

---

## ⚙️ Config File

Location:
~/.tmux.conf

Reload config:
tmux source-file ~/.tmux.conf

---

## 💡 Useful Tips

- Run tmux inside SSH → session stays alive even if connection drops
- Use multiple windows like tabs
- Use panes for split views (code + logs etc.)

---

## 🏁 Exit tmux

exit      # close current pane/session

---

## 🔥 Pro Tip

Change prefix key (example to Ctrl+A):

set-option -g prefix C-a
unbind C-b
bind C-a send-prefix

---

Made for quick reference ⚡
