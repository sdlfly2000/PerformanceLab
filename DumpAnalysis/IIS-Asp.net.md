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

* Display all threads' stacks
> ~* e!CLRStack

* Select thread holding sync block
> !CLRStack

* Find caller with addr
> !ip2md

* IL
> !DumpIL