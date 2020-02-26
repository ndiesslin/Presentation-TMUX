# TMUX - A Terminal Multiplexer

## Speaker: Nick Diesslin
### Twitter handle: @ndiesslin

---

## Key Takeaways

- What is TMUX?
  - Alternatives
- Benefits
- Getting started
- How to configure
- Plugins
- How to use
- Commands
- Use cases
- Expanding upon TMUX, creating widgets

---

## What is TMUX?

- TMUX is a terminal multiplexer
- TMUX runs sessions, sessions contain windows and windows contain panes
- The biggest benefit is being able to run multiple terminal commands at the same time
- TMUX is for UNIX like operating systems

### Alternatives to TMUX

TMUX is recommended, but to be fair there are other terminal session managers available

- Screen (Older GNU terminal session manager)
- Byobu 

## Benefits

- The terminal will now run sessions, which can be detached and attached to a terminal window
- Tabs, split screens in session
- Configurable
- Zooming in panes
- Saved and restored sessions (with plugins)

## Getting Started

- TMUX is available with most package managers
- Mac
``` 
brew install tmux
```
- Debian based linux
```
apt-get install tmux 
```
- Then type tmux to start a session
```
tmux
```
- TMUX has what is called a prefix key, this is the keyboard combination you will need to interact with TMUX. By default it is ctrl+b
```
ctrl+b
```

## How to configure

- TMUX will load configurations based off of the .tmux.conf file in your home directory (~)
- You can steal someone's configuration from the internet to start off in a better place, but you will want to review in case there are any unfamiliar keybindings
- Default tmux command prefix: Most of the users on the internet remap ctrl+b to ctrl+a
- TMUX uses 256 color palette
- To see the colors available for configurations run this script
```
for i in {0..255}; do
    printf "\x1b[38;5;${i}mcolour${i}\x1b[0m\n"
done
```
- Status bar can be beneficial for adding important information, like server uptime or current time.
- This is a great resource for making TMUX more usable: https://www.hamvocke.com/blog/a-guide-to-customizing-your-tmux-conf

## Plugins
- Plugin manager tpm (easier way to manage plugins): https://github.com/tmux-plugins/tpm
- TMUX yank (copying to clipboard): https://github.com/tmux-plugins/tmux-yank
- TMUX resurrect (persistent sessions after restarts): https://github.com/tmux-plugins/tmux-resurrect
- TMUX continuum (continuous saving of tmux environment.): https://github.com/tmux-plugins/tmux-continuum
- TMUX sensible (standardized tmux settings): https://github.com/tmux-plugins/tmux-sensible 

- Full list of plugins here: https://github.com/tmux-plugins

## How to use
- Creating windows
- Splitting windows into panes
- Resizing panes
- Zooming in and out of pane

## Commands

### Sessions

- Load tmux session
```
tmux
```

- Load tmux session with name - beneficial if multiple people work on same machine
```
tmux new -s mysession
```

- Show running tmux sessions
```
ctrl+b s
```

- Detach from session
```
ctrl+b d
```

### Windows/Tabs

- Create new window
```
ctrl+b c
```

- Close current window
```
ctrl+b &
```

### Panes

- Split pane vertically
```
ctrl+b %
```

- Split pane horizontally
```
ctrl+b "
```

- Switching panes
```
ctrl+b (any arrow key for direction)
```

### Copy Mode

- Copy mode puts the session in a mode that allows you to interact with your terminal session in a similar way to vim. This is especially helpful with things like searching logs.

- Enter copy mode
```
ctrl+b [
```

- Arrow up and down to go through lines in sessions, or you can use j to move down or k to move up like in vim.

- Visually select a line
```
Shift+v
```

- Copy highlighted line
```
y
```

### Giant clock
```
ctrl+b t
```

## Use cases
- Comparing multiple servers in split view
- Saving and restoring sessions for saving time with local development
- Multiple users working on same server, each could spin up their own TMUX session
- Creating a session with a command that you can check in on

## Expanding on TMUX

### Creating a status widget

- TMUX can run any script and display this in the status bar. This means you can really use any scripting language to create some sort of status bar widget.

- Simple example of something that could be used in statusbar
```
touch ~/pingtest.sh
```

```
echo "ping google.com" >> ~/pingtest.sh
```

- Add this to statusbar
```
#(sh ~/pingtest.sh)
```

- I've created a simple node weather script that returns the weather to be used in the status bar https://github.com/ndiesslin/TMUX-weather-widget

### Running a command with a TMUX session
- TMUX can be helpful if you need to run a command to check in on later, this could be on a server for example.

```
tmux new-session -d -s temporary_session 'sh ~/pingtest.sh'
```

- Attach to our session we created
```
tmux attach -t temporary_session
```
