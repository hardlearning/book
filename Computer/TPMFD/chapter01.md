# CHAPTER 1 Learning the Basics

## Installing tmux

#### Installing on a Mac

```
xcode-select --install
brew install tmux
tmux -V
```

#### Installing on Linux

```
sudo apt install libevent-dev ncurses-dev build-essential bison pkg-config
tar -zxvf tmux-3.5a.tar.gz
cd tmux-3.5a
./configure
make
sudo make install
tnux -V
```

## Starting tmux

> Creating Named Sessions

```
# Create a named session called “basic”
tmux new-session -s basic
# You can shorten this command to this
tmux new -s basic
# close the session and exit tmux
exit
```

## The Command Prefix

The Ctrl-b combination is called the command prefix.

Throughout the rest of this book, I’ll use the notation PREFIX, followed by the shortcut key for tmux commands, like PREFIX t for showing the clock.

Inside of tmux, press Ctrl-b, then press t. A large clock will appear on the screen. Press the ENTER key to dismiss the clock, and exit tmux by typing exit.

## Detaching and Attaching Sessions

```
# First, create the session
tmux new -s basic
# Start an application called top
top
# Now, detach from the tmux session by pressing PREFIX d
```

#### Reattaching to Existing Sessions

```
# Now create a new tmux session in the background
tmux new -s second_session -d
# list existing tmux sessions
tmux list-sessions
# You can shorten the command to this
tmux ls
# Attach to the second_session tmux session
tmux attach -t second_session
```

#### Killing Sessions

```
# Run the following commands to end the basic and second_session sessions
tmux kill-session -t basic
tmux kill-session -t second_session
```

## Working with Windows

```
# Create a named session called windows
# By using the -n flag, you tell tmux to name the first window so you can identify it easily.
tmux new -s windows -n shell
```

#### Creating and Naming Windows

To create a window in a current session, press PREFIX c.

To rename a window, press PREFIX followed by , (a comma).

#### Moving Between Windows

When you only have two windows, you can quickly move between windows with PREFIX n, for “next window.”

You can use PREFIX p to go to the previous window.

By default, windows in tmux each have a number, starting at 0. You can quickly jump to the first window with PREFIX 0, and the second window with PREFIX 1.

If you end up with more than nine windows, you can use PREFIX w to display a visual menu of your windows so you can select the one you’d like.

You can also use PREFIX f to find a window that contains a string of text.

To close a window, you can either type “exit” into the prompt in the window, or you can use PREFIX &.

## Working with Panes

```
# Create a new tmux session called “panes”
tmux new -s panes
```

In the tmux session, press PREFIX %, and the window will divide down the middle.

Now press PREFIX " (double quote) to split this new pane in half horizontally.

To cycle through the panes, press PREFIX o. You can also use PREFIX, followed by the UP , DOWN , LEFT , or RIGHT keys to move around the panes.

#### Pane Layouts

- even-horizontal: stacks all panes horizontally, left to right.
- even-vertical: stacks all panes vertically, top to bottom.
- main-horizontal: creates one larger pane on the top and smaller panes underneath.
- main-vertical: creates one large pane on the left side of the screen, and stacks the rest of the panes vertically on the right.
- tiled: arranges all panes evenly on the screen.

You can cycle through these layouts by pressing PREFIX SPACEBAR .

#### Closing Panes

You can also kill a pane with PREFIX x, which also closes the window if there’s only one pane in that window.

## Working with Command Mode

To enter Command mode, press PREFIX : (the colon) from within a running tmux session.

```
# Create a new window by using the new-window command
new-window -n console
# Let’s take this a step further and launch a new window that starts the top program.
new-window -n processes "top"
```

## What’s Next?

By pressing PREFIX ?, you can get a list of all predefined tmux keybindings and the associated commands these trigger.