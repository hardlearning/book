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