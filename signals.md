## Signals

Signal is used to notify a process about external events (page fault, interrupt from keyboard) . Except real time signals, normal signals are not queued, kernel keep track of pending  signal for each process as bit mask. Also no other data is associated with signal.

Except KILL and STOP, signals can be blocked, default signal handlers can be ignored and overwritten. Signals can be generated in program using kill, tkill, send_sig.

To suspend a process run e.g.

     kill -SIGSTOP 3878

State of process can be observed by

     ps -eo pid,state,cmd
     
To resume the suspended process run

    kill -SIGCONT 3878

**Default signals**

The default signal sent out by `kill` is `TERM` mean terminate the process. Each process reacts to each signal differently, Java process e.g. dump stacktrace of all threads to stdout unpon receiving `QUIT`.  

**Delivery of a signal**

When sending a signal to a running process (on CPU), the signal is pending until the process is preempted, at that time the signal is delivered to the process and a signal handler is called.

When sending a signal to process in an `interupptible` waiting state, the process is waked up, the signal is delivered to the process and signal a handler is called.

When sending a signal to process in ready state, the signal is delivered to the process and signal a handler is called whenever the process get CPU.

