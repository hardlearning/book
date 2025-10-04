# CHAPTER 2 Configuring tmux

## Introducing the .tmux.conf File

Tmux looks for configuration settings in a few places:

1. /etc/tmux.conf
2. .config/tmux/tmux.conf in the user’s home directory
3. $XDG_CONFIG_HOME/tmux/
4. A file called .tmux.conf in the current user’s home directory

Execute the following command to create the file .tmux.conf in your home directory:

```
touch ~/.tmux.conf
```

#### Defining an Easier Prefix

```
# Set the prefix from C-b to C-a
set -g prefix C-a
```

You’re using the -g switch, for “global,” which sets the option for all tmux sessions you create.

You use the unbind-key, or unbind command, to remove a keybinding that’s been defined so you can assign a different command to this key later.

```
# Free the original Ctrl-b prefix keybinding
unbind C-b
```

You’ll need to enter tmux’s Command mode with PREFIX : and type the following command whenever you make a change:

```
source-file ~/.tmux.conf
```

#### Changing the Default Delay

```
# Set the delay between prefix and command
set -s escape-time 1
```

The -s flag sets tmux Server options, which apply to the entire tmux server and all sessions it manages. The difference between -s and -g is that when you use -s to set options, you can’t override them in a specific session later.

#### Setting the Window and Panes Index

```
# Set the base index for windows to 1 instead of 0
set -g base-index 1
# Set the base index for panes to 1 instead of 0
set -w -g pane-base-index 1
```

The pane-base-index option is a window option, so you should add the -w flag.

## Customizing Keys, Commands, and User Input

#### Creating a Shortcut to Reload the Configuration

Define PREFIX r so it reloads the .tmux.conf file in the current session. Add this line to your configuration file:

```
bind r source-file ~/.tmux.conf
```

Modify your reload command to display the text Configuration reloaded when the configuration file loads:

```
# Reload the file with Prefix r
bind r source-file ~/.tmux.conf \; display-message "Configuration reloaded"
```

To put the command on multiple lines, place the \ character after part of the command, and continue the command on the next line:

```
# Reload the file with Prefix r
bind r \
    source-file ~/.tmux.conf \; \
    display-message "Configuration reloaded"
```

#### Sending the Prefix to Other Applications

```
# Ensure that we can send Ctrl-A to other apps
bind C-a send-prefix
```

After reloading the configuration file, you can send Ctrl-a to an application running within tmux simply by pressing Ctrl-a twice.

#### Define New Keys for Splitting Panes

You’ll set the horizontal split to PREFIX | and the vertical split to PREFIX -.

```
# Split panes with | and -
bind | split-window -h
bind - split-window -v
```

#### Remapping Movement Keys

```
# Move between panes with Prefix h,j,k,l
bind h select-pane -L
bind j select-pane -D
bind k select-pane -U
bind l select-pane -R
```

In addition, you can use PREFIX Ctrl-h and PREFIX Ctrl-l to cycle through the windows:

```
bind C-h select-window -t :-
bind C-l select-window -t :+
```

#### Define Keys to Resize Panes

Use PREFIX H, PREFIX J, PREFIX K, and PREFIX L to change the size of the panes:

```
bind H resize-pane -L 5
bind J resize-pane -D 5
bind K resize-pane -U 5
bind L resize-pane -R 5
```

If you use the -r flag with the bind command, you can specify that you want the key to be repeatable, meaning you can press the prefix key only once and then continuously press the defined key within a given window of time, called the repeat limit.

```
# Pane resizing panes with Prefix H,J,K,L
bind -r H resize-pane -L 5
bind -r J resize-pane -D 5
bind -r K resize-pane -U 5
bind -r L resize-pane -R 5
```

> Can I See a List of Keybindings?

- press `PREFIX ?`
- `PREFIX :` and `list-keys`

#### Handling the Mouse

```
set -g mouse on
# Mouse support - set to on if you want to use the mouse
set -g mouse off
```

## Changing How tmux Looks