# Lock
## Behaviour
    1. Loading page or resources slowly;
    2. High CPU, Low Memory, High Disk
    3. Low CPU (thread lock -- Mutex)
## Tools
    1. TinyGet: simulating the request like JMeter
    2. Adplus: dump process when hang

        > Adplus -quiet -hang -pn w3wp.exe -o d:\dumps

    3. Windbg

## Key Steps
    > .loadby sos clr

    > !threads

    > !syncblk

    // Display all threads' stacks
    > ~* e!CLRStack

    // Select thread holding sync block
    > !CLRStack

    // Find caller with addr
    > !ip2md

    // IL
    > !DumpIL

---
# Memory Leak (String)
## Behaviour
    1. Working slowly, mostly performance issue

## Tools
    1. ProcDump

## Note
    It is not easy to locate the method creating string since all threads have completed and pending for next run.
    
    // Create a full dump when memory > 1000 MB
    > procdump.exe -ma -m 1000 DiagnosticScenarios.exe DiagnosticScenarios.DMP

## Key Steps
    > .loadby sos clr

    > !threads

    // Show all Clr stacks for checking what is running in each thread.
    > ~* e!CLRStack

    // Checking unmanaged heap
    > !dumpheap -stat

    > ！dumpheap -strings

    // Checking managed heap
    > !eeheap -gc

    // Checking who possesses the object
    > !gcroot

    // Turning IP to MD if thread stack is intrested.
    > !ip2md

    // IL
    > !DumpIL