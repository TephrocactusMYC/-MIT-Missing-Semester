# Most of all
The golden rule in programming is that code will not run the way you expect it to, but rather the way you tell it to. Debugging and performance analysis are useful techniques for dealing with flawed and resource-intensive code. Debugging can be done using Printf debugging and logging, while performance analysis can use timers and analyzers. Static analysis tools can help identify issues in the code, while code formatting tools can automatically format the code to conform to common programming language styles. Monitoring tools and analyzers can help understand which parts of a program take up the most time and/or resources so that these areas can be optimized.
# Lec Notes
## Debugging
Learn to use Logger instead of print.

Python Debugger is pdb

The lecture suggests using gdb and lldb for low level programming.

### Specialized Tools

Use strace in Linux.

### Static Analysis

pyflakes, pylint and mypy

shellcheck

## Profiling
Timing is a good choice.

The distinction between Real, User and Sys time is important as wall clock time can be misleading due to other processes running or waiting for events. User + Sys indicates the actual CPU time spent by a process.

- Real - Wall clock elapsed time from start to finish of the program, including the time taken by other processes and time taken while blocked (e.g. waiting for I/O or network)
- User - Amount of time spent in the CPU running user code
- Sys - Amount of time spent in the CPU running kernel code

### CPU
cProfile
### Memory
memory-profiler

### Event
perf

### Visualization
Flame graph

### Resource Monitoring

- **I/O operations** - `iotop` displays live I/O usage information and is handy to check if a process is doing heavy I/O disk operations
- **Disk Usage** - `df` displays metrics per partitions and du displays disk usage per file for the current directory. In these tools the -h flag tells the program to print with human readable format. A more interactive version of du is ncdu which lets you navigate folders and delete files and folders as you navigate.
- **Memory Usage** - `free` displays the total amount of free and used memory in the system. Memory is also displayed in tools like htop.
- **Open Files** - `lsof` lists file information about files opened by processes. It can be quite useful for checking which process has opened a specific file.
- **Network Connections and Config** - `ss` lets you monitor incoming and outgoing network packets statistics as well as interface statistics. A common use case of ss is figuring out what process is using a given port in a machine. For displaying routing, network devices and interfaces you can use ip. Note that netstat and ifconfig have been deprecated in favor of the former tools respectively.
- **Network Usage** - `nethogs` and `iftop` are good interactive CLI tools for monitoring network usage.
If you want to test these tools you can also artificially impose loads on the machine using the stress command.

