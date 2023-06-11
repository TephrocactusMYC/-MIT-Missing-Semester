# Command-line Environment
## Job Control
Shell is using a UNIX communication mechanism called a signal to communicate information to the process.

In Unix-like systems, signals are a way of inter-process communication. The Signal constants defined in Linux system and their explanations can be found in the header file `/usr/include/bits/signum.h`, which are defined as follows:
```
/* Signals.  */
#define SIGHUP          1       /* Hangup (POSIX).  */
#define SIGINT          2       /* Interrupt (ANSI).  */
#define SIGQUIT         3       /* Quit (POSIX).  */
#define SIGILL          4       /* Illegal instruction (ANSI).  */
#define SIGTRAP         5       /* Trace trap (POSIX).  */
#define SIGABRT         6       /* Abort (ANSI).  */
#define SIGIOT          6       /* IOT trap (4.2 BSD).  */
#define SIGBUS          7       /* BUS error (4.2 BSD).  */
#define SIGFPE          8       /* Floating-point exception (ANSI).  */
#define SIGKILL         9       /* Kill, unblockable (POSIX).  */
#define SIGUSR1         10      /* User-defined signal 1 (POSIX).  */
#define SIGSEGV         11      /* Segmentation violation (ANSI).  */
#define SIGUSR2         12      /* User-defined signal 2 (POSIX).  */
#define SIGPIPE         13      /* Broken pipe (POSIX).  */
#define SIGALRM         14      /* Alarm clock (POSIX).  */
#define SIGTERM         15      /* Termination (ANSI).  */
#define SIGSTKFLT       16      /* Stack fault.  */
#define SIGCLD          SIGCHLD /* Same as SIGCHLD (System V).  */
#define SIGCHLD         17      /* Child status has changed (POSIX).  */
#define SIGCONT         18      /* Continue (POSIX).  */
#define SIGSTOP         19      /* Stop, unblockable (POSIX).  */
#define SIGTSTP         20      /* Keyboard stop (POSIX).  */
#define SIGTTIN         21      /* Background read from tty (POSIX).  */
#define SIGTTOU         22      /* Background write to tty (POSIX).  */
#define SIGURG          23      /* Urgent condition on socket (4.2 BSD).  */
#define SIGXCPU         24      /* CPU limit exceeded (4.2 BSD).  */
#define SIGXFSZ         25      /* File size limit exceeded (4.2 BSD).  */
#define SIGVTALRM       26      /* Virtual alarm clock (4.2 BSD).  */
#define SIGPROF         27      /* Profiling alarm clock (4.2 BSD).  */
#define SIGWINCH        28      /* Window size change (4.3 BSD, Sun).  */
#define SIGPOLL         SIGIO   /* Pollable event occurred (System V).  */
#define SIGIO           29      /* I/O now possible (4.2 BSD).  */
#define SIGPWR          30      /* Power failure restart (System V).  */
#define SIGSYS          31      /* Bad system call.  */
#define SIGUNUSED       31
```
Yep, more information in Chinese could be found [here](https://blog.csdn.net/u014470361/article/details/83591513).OR  typing `man signal`.

This section is not important I think.

## tmux

- Sessions - a session is an independent workspace with one or more windows
    - tmux starts a new session.
    - tmux new -s NAME starts it with that name.
    - tmux ls lists the current sessions
    - Within tmux typing <C-b> d detaches the current session
    - tmux a attaches the last session. You can use -t flag to specify which
- Windows - Equivalent to tabs in editors or browsers, they are visually separate parts of the same session
    - <C-b> c Creates a new window. To close it you can just terminate the shells doing <C-d>
    - <C-b> N Go to the N th window. Note they are numbered
    - <C-b> p Goes to the previous window
    - <C-b> n Goes to the next window
    - <C-b> , Rename the current window
    - <C-b> w List current windows
- Panes - Like vim splits, panes let you have multiple shells in the same visual display.
    - <C-b> " Split the current pane horizontally
    - <C-b> % Split the current pane vertically
    - <C-b> <direction> Move to the pane in the specified direction. Direction here means arrow keys.
    - <C-b> z Toggle zoom for the current pane
    - <C-b> [ Start scrollback. You can then press <space> to start a selection and <enter> to copy that selection.
    - <C-b> <space> Cycle through pane arrangements.

## Aliases
Useful things!

such as :
```
alias gs="git status"
alias gc="git commit"
```
## Dotfiles
I think I should set symlinked.

## Remote Machines
**The explanation about SSH in the lecture notes is very friendly to beginners**, but it's somewhat redundant for those who have already studied computer networks.
## others
I do not think such as Command syntax highlighting is important, so I will not use zsh, Alacritty or any other shell framework.
