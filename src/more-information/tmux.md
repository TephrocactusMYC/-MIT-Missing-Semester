# TMUX
Ok, All commands in tmux are triggered by a prefix key followed by a command key . It is funny!

Some useful Keyboard shortcuts that I need to remember.

## Why tmux?
- session handling: detaching from and attaching to sessions helps me with context switching and remote working
- platform independence: I can use tmux on my Macbook, my Linux notebook, servers, Raspberry Pis, you name it.
- customizable: there are many ways I can customize the look and behavior of my tmux environment. And I can sync this across different platforms using a simple dotfile

Tmux is a terminal multiplexer that allows you to start multiple terminal sessions.

When using the command line, we open a terminal window and start a session to execute commands such as "npm run dev". When we close this terminal window, the session ends and the "npm run dev" service session is also closed. Sometimes we want our running services like "npm run dev" or some cd commands to be preserved instead of manually executing them again after closing and reopening the window. This is where tmux comes in handy.

It decouples sessions from terminal windows. Closing and reopening a terminal window does not terminate the session; it continues running in execution. Sessions are completely separated from terminal windows.

## WINDOW? SESSION?
*The following content is from this [website](http://ruanyifeng.com/blog/2019/10/tmux.html).*

The typical usage of command line is to open a terminal window (hereinafter referred to as "window") and enter commands in it. This temporary interaction between the user and the computer is called a "session".

An important feature of a session is that the window is connected to the processes launched within it. When you open a window, the session begins; when you close the window, the session ends, and all processes within that session will terminate regardless of whether they have finished running.

A typical example would be logging into a remote computer via SSH and opening a remote window to execute commands. If there's suddenly an interruption in network connection, when you log back in again, you won't be able to retrieve your previous command execution because the previous SSH session has already ended along with its associated processes.

To solve this problem, sessions can be "unbound" from windows: when a window closes, instead of terminating the session altogether, it continues running until another window binds itself to it at some point in time.
### The function of Tmux.
Tmux is a tool that "unbinds" sessions and windows, completely separating them.

(1) It allows accessing multiple sessions simultaneously in a single window, which is useful for running multiple command-line programs at the same time.

(2) It can let new windows "join" existing sessions.

(3) It allows each session to have multiple connected windows, so multiple people can share the session in real-time.

(4) It also supports arbitrary vertical and horizontal splitting of windows.

For example:

```shell
┌─[myc@ubuntu22]─[~]
└──╼[23:40:14]$ tmux
[exited]
┌─[myc@ubuntu22]─[~]
└──╼[23:40:17]$ tmux ls
0: 1 windows (created Sat Jun  3 23:20:57 2023)
┌─[myc@ubuntu22]─[~]
└──╼[23:40:21]$ tmux kill-session -t 0
┌─[myc@ubuntu22]─[~]
└──╼[23:41:06]$ tmux ls
no server running on /tmp/tmux-1000/default
┌─[Fail][myc@ubuntu22]─[~]
└──╼[23:41:09]$
```
## Pane
Tmux can also divide windows into multiple panes, each running different commands. The following commands are executed in a Tmux window.

## Personal understanding.
My personal understanding is that in the default system, the terminal window and session are bound together. When you close this window, the session bound to it will also be closed. However, tmux can preserve this session. As for panes, they are operations that separate windows and correspond to the same session. This should involve concepts related to low-level operating system processes.




