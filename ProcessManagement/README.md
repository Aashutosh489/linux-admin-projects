Linux Process Management

In Linux, everything is a process – a program running in memory.
 Example: When you open a browser, it becomes a process.
 Each process has a PID (Process ID).
Process management means creating, scheduling, monitoring, and killing processes.
Process States in Linux
A process can be in different states:

1. Running (R) – The process is currently executing on CPU.
Example: A program you are actively running.

2. Sleeping (S) – The process is waiting for some event (I/O, user input).
Example: A text editor waiting for you to type.

3. Stopped (T) – The process has been stopped (paused) by a signal.
Example: Press Ctrl+Z to pause a program.

4. Zombie (Z) – Process finished but still has an entry in the process table (not 
cleaned by parent).
Example: A terminated process whose parent hasn’t collected its exit status.

5. Idle / Waiting (I) – Kernel threads waiting for events.

6. Defunct – Same as zombie (dead process but entry remains).

:Important Process Commands
<<<<<<< HEAD
Command              Purpose                        Example
Ps              Show process status                  ps -ef
top            Live view of processes                 top
htop         Advanced top (if installed)              htop
jobs          Show background jobs jobs
fg            Bring job to foreground                 fg %1
bg            Run job in background                   bg %1 
kill         Kill a process                        kill -9 PID
nice     Start a process with priority           nice -n 10 command
=======
Command               Purpose                        Example
Ps               Show process status                 ps -ef
top            Live view of processes top
htop          Advanced top (if installed)            htop
jobs          Show background jobs jobs
fg            Bring job to foreground                fg %1
bg           Run job in background                   bg %1
kill           Kill a process                       kill -9 PID
nice      Start a process with priority          nice -n 10 command
>>>>>>> f570cbf (README.md)
renice   Change priority of running process      renice -n 5 -p PID

:Reserved Process IDs

 PID 0 → Kernel process (scheduler)
 PID 1 → init (first process, parent of all)
 PID 2 → kthreadd (kernel thread handler)
These are system processes and cannot be killed.

Common Commands for Process Management

1. ps – Show processes
 Example:
 Ps
 Ps -a
 ps -ef
 ps -aux

:Kill Command

kill is used to send signals to processes.

 kill -l → Shows all available signals.
Common signals:

 9 (SIGKILL) → Hard kill (forcefully stops process, cannot be ignored).

 15 (SIGTERM) → Soft kill (default, gives process a chance to terminate safely).
Example:
kill -15 1234 # Gracefully stop process with PID 1234
kill -9 1234 # Forcefully kill process

:top Command (Process Monitoring)

top shows real-time process information.

Fields explained:

 PID – Process ID

 USER – Owner of process

 PR – Priority

 NI – Nice value (priority modifier)

 VIRT – Virtual memory used

 RES – Resident memory (RAM used)

 SHR – Shared memory

 S – State (R=Running, S=Sleeping, Z=Zombie, T=Stopped)

 %CPU – CPU usage

 %MEM – Memory usage

 TIME+ – Total CPU time used

 COMMAND – Process name

Use q to quit.

free Command (Memory Usage)

Shows available and used memory.

Example:

free –m  showing date in Mb
free –g  showing date in Gb

Output fields:

 total – Total memory
 used – Memory in use
 free – Unused memory
 shared – Memory shared between processes
 buff/cache – Memory used for buffers and cache
 available – Memory available for new processes

:nice Command (Process Priority)

 Linux assigns a priority to processes.
 Range: -20 (highest priority) → +19 (lowest priority).
 Default nice value = 0.
Examples:

nice -n 10 yes # Start yes with lower priority
renice -n -5 -p 1234 # Increase priority of process with PID 1234

Types of Processes

1. Foreground process – runs directly in the terminal, you interact with it.
o Example:
o vi myfile.txt
Here, vi runs in the foreground.

2. Background process – runs in the background, doesn’t block the terminal.

2. top – Live process monitoring

 Example:
 top
Displays running processes, CPU and memory usage in real time.
(Press q to quit.)

3. kill – Stop a process

 First, find the PID (Process ID) using ps or top.
 Example:
 kill 1234
(This stops the process with PID 1234.)
 Force kill if it doesn’t stop:
 kill -9 1234

4. jobs – Show background jobs

 Example:
 sleep 100 &
 jobs
sleep 100 & runs in background, and jobs shows it.

5. fg and bg – Control background/foreground

 Example:
 sleep 100 &
 fg %1
Brings job 1 to foreground.
bg %1
Sends job 1 to background again.
