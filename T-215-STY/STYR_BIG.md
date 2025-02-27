---
aliases:
---
-------




Operating system (OS) (virtual machine) (resource manager)
- layer between application and hardware to make system easy to use
- Takes a physical resource and virtualizes it
	- physical resource (processor, DRAM, hard drive)
	- virtualization (transform into a virtual form of itself)
- The operating system is a resource manager
	- hides hardware details behind interfaces
		- system calls -> acts as a standard library
	- Provides abstractions for each resource
	- makes hardware use efficient for applications (cost, time, energy)
	- provides protection
		- isolation (prohibit processes changing / reading the state of others)
		- prevent exploitation of OS services
	- Sharing time and space
		- multiplexing hardware to multiple running applications
			- allow and control shared use of a resource
		- Control execution of applications
		- prevents improper use of the computer
- Resources
	- CPU
	- memory
	- disk
- Concepts
	- abstractions (how much of the hardware should be exposed)
	- mechanisms   (implementation of what is done)
	- policies     (rules which decide when & what is done where & how fast)
- A body of software responsible for making it easy to run programs, allowing programs to share memory, enabling programs to interact with devices and much more.
- Takes physical resources, such as CPU, memory, or disk, and virtualizes them
- handles concurrency issues
- stores files persistently
- Goals
	- provide high performance (minimize overheads of the OS)
	- Provide protection between applications (and the OS as well) -> isolation
	- Provide reliability (if OS fails, then all applications fail)
Major tasks of an operating system
- abstraction / standardization
- resource management
- security/protection
- execution environment for applications

Policies
- Intelligence in the OS
- algorithms for making some kind of decision within the OS
- f.x. scheduling policy
- Strictly separate from mechanisms, so that one could switch policies without switching the mechanism.

Scheduling policy
- given a number of possible programs to run, which to choose?
- make decision based on 
	- historical information
	- workload knowledge
	- performance metrics


Mechanisms
- low-level machinery
- low-level methods or protocols that implement a needed piece of functionality
- f.x. context switch


Abstractions
CPU
- time sharing
- Central processing unit
- Main memory and registers are the only storage that the CPU can access directly

Main memory
- the only storage that the CPU can access (except for registers)

Multiple processes can be run concurrently even without memory abstraction
- swapping 
	- a process owns the entire physical user space
	- what
		- save program state on background storage (roll-out)
		- replace with another program's state (roll-in)
	- Benefits
		- only needs hardware support to protect the kernel, but not to protect accesses from one another
	- cons
		- very slow
			- a major part of swap time is stransfer time -> directly proportional to the amount of memory swapped
		- At every point in time, only one process runs (no parallelism)
		- if overlay, need to partition program manually into blocks
- static relocation
	- OS adds a fixed offset at every address in a program when loading it and creates a process from it
	- Can load multiple processes
	- Same address space for every process
		- no protection
		- inefficient use of memory


Sharing physical memory
- desired properties
	- protection
		- a bug in one process must not corrupt memory in another
		- don't allow process to peek into other processes' memory
	- transparency
		- A process shouldn't require particular physical memory addresses
			- the user program deals with virtual addresses so it never sees the real physical addresses
		- processes should be able to use large amounts of contiguous memory
	- resource exhaustion
		- Allow that sum of sizes of all processes is greater than physical memory

Pure Base and limit registers
- Provide basic protection
- On every load / store the MMU
	- checks if address is larger or equal to base
	- checks if address is smaller than base + limit
	- use the CPU address as the physical address in memory
- Main memory split into two partitions 
	- OS and user processes
	- OS can access all process partitions 
	- MMU denies processes access to OS memory (or any memory that is not its own)
- Benefits
	- straight forward to implement MMU
	- very quick at run-time -> only two comparisons necessary
- Cons
	- growing a process' address space is hard
	- sharing code or data is hard

Base and limit registers with relocation
- address is 0 -> limit , then relocates in pmem

Segmentation
- Using multiple base and limit register paris per process
- Virtual address consists of 
	- segment number
	- offset
	- (encoded in the address)
- Each process (address space) has a segment table that maps virtual address to physical addresses in memory
- Each segment has
	- base -> starting physical address where the segment resides in memory
	- limit -> length of segment
	- protection -> access restriction (read/write) to make safe sharing possible
- MMU has two registers that identify the current address space
	- segment-table base register (STBR) -> points to the segment table location of the current process
	- Segment-table length register (STLR)
		- indicates the number of segmends used by the proces
		- i.e. segment number is legal if it is < STLR
- Benefits
	- dynamic relocation is possible
		- compaction is also possible (but not necessarily feasible)
	- makes data / code sharing between processes possible without compromising confidentiality and safety/security
	- process doesn't need one large contiguous physical memory area 
		- easier to place in memory
	- don't need entire process in memory
	- enables isolation of address space
	- enables memory over commitment
- Cons
	- segments need to be kept contiguous in physical memory
	- external fragmentation of physical memory tends to occur


Paging
- page frames
	- divide pmem into fixed-sized blocks called page frames
- pages
	- virtual memory is divided into blocks called pages
- Page table
	- stores mappings between virtual page numbers and page frame numbers per AS
- Role of OS
	- keep track of all free frames
	- modify page tables as needed
- The OS Performs all operations that require semantic knowledge
	- page allocation/ bringing data into memory
		- find free page
		- set up mapping in page table
	- page replacement
		- when all page frames are in use the OS evicts pages from memory to make room for new pages
			- drop and re read from disk on next use
			- save to pagefile or swap area before the frame can be evicted
	- Context switch
		- Set MMU base register to point to the page table of the next process's address space
- Fixed-size allocation of chunks instead of variable-sized segments
- benefits
	- no external fragmentation
- cons
	- internal fragmentation may become a problem (because of the fixed size)
	- naive paging is slow
		- every load / store requires multiple memory references
		- solve by using TLB (a cache that stores recent memory translations)


Memory mapped file IO 
- allows file IO to be treated as routine memory access by mapping a disk block to a page in memory
	- file initially read using demand paging.
	- page-sized portion of file is read from file system into physical page
	- subsequent reads/writes to/from the file are treated as ordinary memory accesses
- simplifies file access by treating file IO through memory rather than read / write system calls
- Allows several processes to map the same file allowing the pages in memory to be shared

Shared data segments
- often implemented with
	- temporary, anonymous, memory-apped files
	- shared pages (with allocated space on backing sotre)
		- different vaddresses can point to the same paddress

Copy on write COW
- allows multiple processes to initially share the same pages in memory
	- a page is copied only if one of the processes attempts to modify it
	- COW allows more efficient process creation as only modified pages are copied.
- If a paddress is referenced by many vadresses then then they can all read the same paddress, then when one writes to it, we copy the page

Page size trade-offs
- fragmentation
- page table size
	- larger pagees 
		- fewer PTEs
			- fewer bits needed for pfn and more for offset
		- More data needs to be loaded form disk to make page valid
		- more internal fragmentation
		- need fewer TLB entries per memory
	- smaller pages
		- more and large PTEs
		- on average only half a page wasted for every allocation
		- need to trap OS more often when loading large program (for IO request)
- \*page table hierarchies suppoort multiple page sizes with uniform entries
	- allows applications that map larger memory areas to increase TLB coverage with minimal increase in fragmentation

Frame allocation
- Global allocation
	- All frames are considered for replaement
		- does not consider page ownership
		- one process can get another process's frame
		- does not protect process from a process that hogs all memory
- local allocation
	- Only frames of the faulting process are considered for replacement
		- ioslates processes (or users)
		- separately determine how many frames each process gets
- equal allocation
	- all processes get the same amount of frames
- Proportional allocation
	- Allocate according to the size of the process
- Priority allocation (global replacement)
	- proportional allocaion scheme using priorities rather than size
	- if process Pi generates page fault
		- select a frame that it, or a process with a lower priority, owns for replacement


Extending memory using background storage
- paging extends memory size using background storage
	- background storage is much slower than memory
- Goal
	- Keep the most used 10% of memory, in memory, rest on disk

Tharshing
- if total demand for frames is greater than physical memory, then thrashing has occurred

Keeping track of the working set
- Total number of pages referenced in the most recent delta
- The MMU automatically sets the reference bit in the respective page table entry every time a page is referenced
- How to manage
	- set timer to scan page table entries for reference bits


Page fetch policy
- Demand paging
	- Transfer only pages that raise page faults
	- benefits
		- only transfer what is needed
		- less memory needed per process (higher degree of multiprogramming possible)
	- cons
		- many intial page faults when a task starts
		- more IO operations -> more IO overhead
- pre paging
	- speculatively transfer pages to RAM
	- At every page fault, speculate what else should be loaded 
		- (e.g. load entire section when starting proceess)
	- benefits
		- improves disk IO throughput by reading chunks
	- cons
		- wastes IO bandwidth if page is never used
		- can destroy the working set of other processes in case of page stealing




Pareto principle
- 10% of memory gets 90% of the references
- (applies to working sets of processes)

Page table
- composed of page table entries PTEs
- Each PTE stores some data
	- Present bit
		- indicates if a virtual apge is currently mapped to physical memory
	- page frame number (PFN)
		- base address of page pointed to
- MMU reads the page table to autonomously translate valid mappings
	- if a mapping does not exist, the MMU calls the OS to bring in the data (via page fault)
- virtual address
	- virtual page number VPN
		- index into page table (to find base address of the page pointed to)
	- page offset
		- concatenated with page frame number which results in physical address
		- i.e. base address + offset = paddress
- types
	- linear page table
	- multi-level page table
	- inverted page table

Page table entry PTE in detail
- valid bit / present bit
	- whether a page is currently available in memory or needs to be brought in by the OS (via page fault)
- Page frame number
	- if page is present, at which physical address is the page located
- write bit
	- if page may be written to (write permission)
- accessed bit
	- if page was touched since the bit was last cleared
- dirty bit
	- set if page was modified since the bit was last cleared by the OS
![Screenshot 2024-04-14 at 14.36.22.png](../images/Screenshot%202024-04-14%20at%2014.36.22.png)

Linear page table
- A page table with one entry per virtual page number
- stores (per PTE)
	- valid bit
		- some VPN may not exist in physical memory
	- physical frame number
- bad
	- keep complete page table in memory for each process
	- most virtual addresses are not used by process
		- there's no need to store invalid vpns

two-level page table
- Page table itself can be paged to save memory
	- VPN is subdivided
		- page directory
		- PTE

Linear inverted page table
- Map physical frame to virtual page instead of other way around
- single page table for all processes (exactly one table per system)
- one page table entry for each physical page
- benefits
	- less overhead for page table meta data
- cons
	- increases time needed to search the table when a page reference occurs

hashed inverted page table (hash anchor table)
- limits the search to very few page-table entries on average
- hash into hash anchor table
	- Search collision resolution table (collisions chained here)


%CR3
- CPU register with address of start of page table -> first level page table


Fragmentation
- The inability to use free memory
- External fragmentation
	- sum of free memory satsifies requested amount of memory.
	- requests cannot be fulfilled with contiguous memory
- Internal fragmentation
	- overallocating resources requests to align memory blocks
	- don't have free blocks left although there is sufficient unused memory within the blocks
- Three factors required for fragmentation to occur
	- different lifetimes
		- symmetric allocation times -> stack
	- different sizes
		- predictable size (no internal) + no external
	- inability to relocate previous allocations

Compaction
- reduces external fragmentation
	- close gaps by moving allocated memory in one direction
	- results in a large free block on the other side
	- compation is possible only if relocation is dynamic, and can be done at execution time.

Overlays
- if process you want to run needs more memory than available

Physical memory (memory) (pmem)
- An array of bytes.
- to read memory, one specifies an address
- to write (or update memory) one must add the data to be written
- a shared resource managed by the OS
- space sharing

Disk
- For persistence
- Not virtualized -> mainly used for shared data


Multiplexing
- a technique used to combine and send the multiple data streams over a single medium

OS interfaces 
- allows users to the the OS what to do and make use of the virtual machine
- f.x. syscalls

OS abstraction examples
- CPU -> processes / threads
- Memory -> address space
- disk -> files

Virtualizatin
- make each application believe it has each resource to itself
- take a physical resource and transform it into a more general, powerful, and easy to use virtual form of itself
- makes the system easier to use


Concurrency
- events are occurring simultaneously and may interact with each other
- what needs to be done?
	- hide concurrency of independent processes (don't know)
	- manage concurrency with interacting processes
- multiple processes can coexist in a system
- multiple processes run on the same CPU (f.x. in a round-robin fashion)
- The host of problems that arise and must be addressed when working on many things at once (cuncurrently) in the same program.

Parallelism
- multiple processes truly running at the same time with multiple CPUs

Persistence
- Information can be accessed permanently : the lifetime of information of exceeds the lifetime of any one process
- The abstraction provided by the OS of a running program
- at any tiem can be summarized by taking an inventory of the different pieces of the system it accesses or affects during the course of its execution

Process
- a program in execution (instance of a program)
- Each associated with an OS data structure called PCB
- The machine state indicates what's important to the execution of the process.
- Provide the abstraction of an address space and resources
- each process has
	- it's own address space
	- it's own set of allocated resources
	- threads of execution -> abstraction of execution states of that AS

Process API
- create
- destroy
- wait
- miscellaneous control
	- f.x. suspend process
- status
	- status info -> how long has run, what state currently?


Multiple processes vs. multiple threads
- Multiple processes
	- rarely share data except explicitly
- multiple threads
	- closely related activities share data which favors threads

Process vs. threads
- Processes group resrouces
- threads encapsulate execution

Process control block PCB
- information needed to implement processes
- Always known to the OS
- Typical items
	- Address space
	- open files
	- child processes
	- pending alarms

Thread control block TCB
- Per thread data
- Known by the OS if Kernel level thread, else not
- typical items
	- instruction pointer
	- registers
	- stack
	- state

Thread model
- The OS kernel always knows of at least one thread per process
	- Kernel level threads

Kernel level threads KLT
- Threads that are known to the OS

User level threads ULT
- known to the process
- Threads that are fully implemented in user-space

Many-to-one model
- Kernel knows only one of possibly multiple threads in a process
- threads fully implemented in user space
- Kernel only manages process -> multiple threads unknown to kernel
- Threads managed in user-space library
- benefits
	- faster thread management operations (up to 100 times)
	- flexible scheduling policy
	- few system resources
	- can be used even if the OS does not support threads
- Cons
	- no parallel exe cution
	- whole process blocks if only one user thread blocks
	- need to re-implement parts of the OS (thread switching)
- How
	- thread must yield itself
	- can also be implement using SIGALRM signal handler
- Address space layout
	- Stacks for each thread implemented in heap
	- stack known to the OS used for the user thread library (managing the threads)

One-to-one model
- Each user thread maps to a kernel thread
- Kernel knows and manages every thread
- all thread management data is stored in kernel
- thread management functions are provided as syscalls
- on fork -> only forking thread propogates, all other threads eliminated
- benefits
	- real parallelism possible
	- threads block individually
- cons
	- OS manages every thread in the system (TCB, stacks, etc.)
	- syscalls needed for thread management
	- scheduling fixed in OS 
	- more context switching
- address space layout
	- stacks disconnected from heap (as many stacks as threads)

M-to-N model (hybrid thread model)
- Kernel knows of multiple threads per process, but there are even more threads konwn to the process itself
- flexible mapping of user threads to les kernel threads
- Goal
	- pros of ULT and KLT
		- non-blocking with quick management
		- create a sufficent number of KLTs
		- Flexibly allocate ULTs on those KLTs
- Pros
	- flexible scheduling policy
	- efficient execution
- cons
	- hard to debug
	- hard to implement
- how
	- upcalls
		- a mechanism that allows the kernel to execute a function in user space
		- if the kernel notices that a thread will block, sends upcall to process
		- upcall notifies th eprocess of th thread id and event that happend
		- upcall handler of the process can the n schedule a different thread in that proces
		- kernel later informs the process that the blocking event has finished via another upcall


Machine state
- what a program can read or update when it is running -> important to the execution of the process
- components
	- memory -> address space
	- registers
	- I/O information, such as list of open files

Signals
- notify a process that a particular event has occurred
- signal handler can run
	- on the process stakc
	- on a stack dedicated to the specific signal handler
	- on a stack, dedicated to all signal handlers
- Whom is the signal delievered to
	- really unclear
	- Subscribing to a signal

SIGALRM
- process can ask OS to send SIGALRM after specific time



Process creation
- four events cause processes to be created
	- system initialization (booting)
	- process creation syscall (issued by a running process)
	- user request to create a new process
	- initiation of a batch-job
- Map to the same two mechanisms
	- kernel spawns the initial user space process on boot
	- user space processes can spawn further processes (within their quota)
		- (fork in posix)
- process acc to book
	- load code and static data into memory (in the vAS) -> read from disk into memory
		- often lazy loading in modern systems
	- Allocate memory for run-time stack and fill main parameters
	- allocate memory for heap
	- initialize file descriptors
		- in
		- out
		- error
	- Jump to main and transfer control of CPU to the newly-created process


Process state
- running -> running on a processor / executing instructions
- ready   -> ready to run, but OS has chosen not to run for the moment
- blocked -> process has performed some kind of operations and is not ready to run until some other event has occurrred.


Fork (process creation)
- pid = fork()
	- duplicates current process
	- returns 0 to the resultant child
	- return child's process PID to parent
- PID -> identifies process
- exec(name) 
	- to replace own memory based on an executable file (name -> name of a binary executable file)
- exit(status)
	- terminate the process and return exit status
- pid = wait(&status)
	- wait for termination of one of its children
	- status points to an integer bit field that returns information about the process
	- child's pid returned on success, otherwise -1 (on fail)
- Process tree
	- where children spawn multiple iterations of new processes
- parent and children share resources (parts of the address space)
	- all descriptors open in the parent are shared with the children
		- connected socket f.x.
- parent and children execute concurrently
- also copies file descriptors
	- but they still point to same element in the global open files table, thus they manipulate each others lseek

reentrant / recursive mutex
- a variant of mutex that can be locked multiple times by the same process without causing a deadlock
- only becomes available after equally many unlocks

exec
- execve
- execv


main arguments
- argc -> number of arguments
- argv (envp) -> argument and environment vector pointers
	- execv -> envp = NULL
	- environment is typically defined by your shell

cron Daemon (linux)
- started on boot
- starts batch jobs defined in cron table crontab

Daemons
- processes designed to run in the background
- detached from their parent process after creation
	- create new session using setsid in C
- usually reattached directly to the root of the process tree (init)

Process termination
- 4 events cause processes to terminate
	- voluntary
		- normal exit
			- return 0 or exit(0)
		- Error exit 
			- return x, exit(x) or abort()
	- Involuntary
		- Fatal error
			- OS kills process after exception
			- process exceeds allocated resources
		- killed by another process
			- another process sends a signal to kill the process
			- only with permission (parent process, or admin privileges)
			- kill(pid, -9) -> man 7 signal


allotted resources
- man ulimit


Exit status
- voluntary exit
	- return integer (only last 8 bites on linux)
	- Process resources cannot be completely free'd after a process terminates
		- results in a zombie process or process stub, can deliver ext status, remains until collected via waitpid- > only 
- Involuntary exit
	- bits 0-6 : signal number that killed the process (0 on normal exit)
	- 7        : set if process was killed by a signal
	- bits 8-15: 0 if kille dby signal (exit status on normal exit)

Zombie process (process stub)
- what remains of a process after it terminates
- waits until exit status is collected via waitpid
- once collected the PID is freed and all resources deallocated

Orphans
- children that keep running after their parent exits
	- init generally adopts orphans (so they keep running)
- possible: cascading termination (kill all children when parent exist)

pstree -a
- check out the process structure

Program control block (PCB)
- The individual structure that stores information about a process

Execution stream
- sequence of executed instructions

Process state
- everything that the running code can affect or be affected by
- includes
	- registers
	- address space
	- I/O state

Multiprogramming
- 
- Implemented using concurrency and parallelism

Concurrency vs. parallelism
- multiple processes run on the same CPU (f.x. in a round-robin fashion)
- Processes truly running at the same time with multiple CPUs


Direct execution
- allow user process to run directly on hardware
- OS creates process and transfers control to starting point
- Problems
	- Processes are not monitored in any way
		- read/write other process data
		- process could run forever

Limited Direct Execution (LDE)
- OS creates process and transfers control to starting point
- privilege level
	- changed through system call (trap instruction)
- two CPU modes of execution (bit of status)
	- user mode (restricted)
		- runs user processes
	- kernel mode (not restricted)
- User processes have their own address space
- Kernel memory is protected from user mode references
- Interrupts
	- notifications from timers and I/O devices
	- OS can preempt a process

Modes of execution -> LDE
- User mode (x86: CPL3 / ring 3)
	- non-privileged instructions only
	- cannot manage hardware (protected)
- Kernel mode (x86: CPL0 / ring 0)
	- All instructions allowed
	- manages hardware with privileged instructions
- Modern CPU modes
	- Hypervisor
	- System management mode

Address spaces
- A virtual memory abstraction
- Every process has a virtual address space
	- see address space layout
- MMU
	- relocate each load/store to physical memory
	- processes never see physical memory and cannot address it directly
	- Enforces protection
	- Programs see more memory than available
		- i.e. what's loaded into memory 
- Benefit
	- can keep working set in RAM and rest on disk, the n relocate dynamically
		- 80 % of the process memory is idle 20% is active (most of the time)
- con
	- overhead of needing MMU hardware


Adress space layout
- code, data, and state need to be organized within the address space
- three kinds of data
	- fixed size data items
	- data that is naturally free'd in reverse order of allocation
	- data that is allocated and free'd dynamically (at random)
- loader
	- determines based on executable file, how an executed program is placed in memory
- The compiler (linker) and os (loader) decide where to place which data and how many segments exist.
![Screenshot 2024-03-21 at 16.28.18.png](../images/Screenshot%202024-03-21%20at%2016.28.18.png)
![Screenshot 2024-03-21 at 16.41.52.png](../images/Screenshot%202024-03-21%20at%2016.41.52.png)

Fixed size data and code segments
- Memory that can be statically allocated when the process is created
	- data that never changes and data that will be written but never changes in size
- Segments
	- Data segment
	- read-only data segment
	- Block started by symbol segment (BSS segment)
	- (the BSS data and read-only data segments are sometimes summarized as a single data segment)


Stack segment
- data that is naturally free'd in reverse order of allocation
- easy memory management (stack grows downwards)
- how
	- fixed starting point of segment
	- uses stack pointer to store bottom of latest allocation (initialized to starting point)
	- Allocate new byte data structure with push CPU instruction
	- Free a byte data structure with pop CPU instruction

Heap segment (Dynamic memory allocation )
- Data that needs to be allocated and free'd dynamically at runtime (randomly)
- two tiers
	- allocate heap segment from OS (large chunk of memory)
		- base address + break pointer
		- process can get more memory from OS or give back memory by setting BRK using a system call (sbrk())
		- kernel mode
	- Dynamically partition heap segment into smaller allocations
		- malloc and free
		- happens purely in user space (don't need to contact kernel)

Dynamic memory alloction
- allocate and free memory chunks of "arbitrary size" at arbitrary points in time
	- e.g. heap
	- Data doesn't have to be specified statically
- Implementation has a huge impact on performance
	- But impossible to construct a memory allocator that always performs well

Dynamic memory allocator
- Initially has a pool of free memory
- needs to
	- satisfy arbitrary allocate and free requests from that pool
	- track which parts are in use and which parts are free
- cannot move allocatd regions (no compaction)
	- relocation is not possible, and bad allocation decisions are permanent
- Issues
	- fragmentation
		- external and internal


Known patterns of real programs
- patterns
	- ramps -> only going up
		- accumulate data monotonically over time
		- very few frees
	- peaks  -> triangles
		- allocate many objects, use briefly, then free all
		- fragmentation is more likely to occur
	- plateaus -> trapizoid
		- allocate many objects, use for a long time
- Segregation
	- if allocated at same time, and then freed at the same time (or just about), there's less fragmentation

Bitmap 
- divides memory in allocation units of fixed size
- keeps track of allocated or free (1 or 0)
- needs additional data structuree to store allocation length
	- otherwise cannot infer whether two adjacent allocations belong together or not from bitmap, but need this info for free

list 
- one list node, or one for each allocated area
	- need extra space for list
	- can provide info about storage allocation length

free-list
- one list-node for each unallocated area (free list)
	- keep list in unallocated area (store size of free area and pointer to next free area, can search for free space with low oeverhead)
- put list element in the unused memory block itself
- for used blocks
	- have header, track size information, embed header in allocated block

Fitting
- decide where to place the new block
- Keep large free memory chunks together for larger allocation requests that may arrive later
- Best fit
	- allocate the smallest free block that is large enough to fulfill the allocation request
	- must earch entire list (unless ordered by size)
	- during free (coalesce adjacent blocks)
	- Problems
		- sawdust
			- external fragments of allocations are so small that over time leftovers with unusable sawdust are everywhere
- Worst fit
	- allocate the largest free block -> same properties, but worse fragmentation than best fit
- first fit
	- optimize for allocation speed
	- allocate to the first hole that is big enough
	- produces leftovers of variable size
	- Almost as good as best fit
	- types
		- sorted by address order
			- blcoks at front preferentially spolit, one at back only split when no larger one found before them
			- seems to roughly sort free list by size
			- similar to best fit
			- sorting of list forces a large request to skip over many small blocks
		- LIFO first-fit
			- put object on front of list
			- cheap & fast allocation policy
			- hope same size is used again
		- next-fit
			- remember where you found the last thing to start searching
			- tneds to break down entire list -> bad cache locality

SLAB allocator
- kernel often allocates / frees memory for few specific data objects of fixed size
	- kernel data object
- slab is made up of multiple pages of contiguous physical memory
- a cache consists of one or multiple slabs
- each cache stores only one kind of object (fixed size)
- linux uses buddy alloctor as underlying allocator for slabs

Stack pointer (SP)
- a register that stores the location of the latest allocation in the stack.
- lower-most address of stack segment

Frame pointer (FP)
- also helps with stack memory

Program break pointer (BRK)
- upper-most address of heap segment (limit)

instruction pointer (IP)
- an address in text segment (actual program code)


Program status word (PSW)
- contains flags about the execution history
- e.g. last calculation was zero

Data segment
- initialized data elements

read-only data segment
- constant numbers and strings

Block started by symbol segment (BSS segment)
- includes
- variables that have not been initialized
- an executable file typically contains the string address and size of BSS
- the entire segment is initially zero

Instruction privilege


System call dispatcher
- acts as a multiplexer for all syscalls



trap instruction
- Switches the CPU to kernel mode (LDE)
- Enters the kernel in the same, predefined way for every syscall
- The only entry point (system call interface) into the kernel
- Syscalls are identified by a number which is passed as a parameter
- ![Screenshot 2024-03-21 at 17.05.39.png](../images/Screenshot%202024-03-21%20at%2017.05.39.png)


System call table
- maps system call numbers to kernel functions
- The dispatcher decides where to jump based on the number and table
- Program
- ![Screenshot 2024-03-21 at 17.13.43.png](../images/Screenshot%202024-03-21%20at%2017.13.43.png)

Dispatcher (mechanism)
- allocates system resources to different processes
- Ensure that all processes running on the system receive the necessary resources in a fair and efficient manner, minimizing the waiting time and maximizing the system throughput
- Works closely with the process scheduler
	- But can work with different schedulers (hence the separation of the two (policy / mechanism))
- in syscalls: Looks up syscall number and calls correct handler
- Performs actual process switch (context switch)
	- saves / restores process context
	- switches user modes

The CPU Scheduler (policy)
- selects the next process to run
- Goals
	- efficiency
	- fairness
	- adhering to priorities

Short-term scheduler
- selects which process should be executed next and allocates CPU 
	- selects from ready queue
	- must be very efficient
- short-term scheduler is invoked frequently and must be very fast
- A number of different policies to choose from

Long-term scheduler (job scheduler)
- selects which process should be brought into the ready queue
- long-term scheduler is invoked very infrequently (seconds or minutes)
- controls the degree of multiprogramming
- Decides which jobs to load into memory and prep for execution
- found on job-processing systems rather than regular desktops

Process scheduling queues
- job queue
	- a set of all processes in the system
- ready queue
	- processes in main memory 
- device queues
	- processes waiting for an IO device

Categories of scheduling policies
- Batch scheduling
	- No users waiting for quick response
	- non-preemptive algorithms, less switches and therefore less overhead
	- Goals
		- Throughput
			- number of processes that complete per time unit
		- Turnaround time
			- time from submission to completion of a job
		- CPU utilization
			- Keep the CPU as busy as possible
	- Bad for
		- batch scheduling suffers from starvation and does not provide fairness
- Interactive scheduling
	- Optimized for response time
	- preemption essential to keep processes from hogging CPU
	- Goals
		- Waiting time
		- response time (from request to first response)
- real-time scheduling
	- Guarantee completion of jobs within time constraints
	- Need to be able to lan when which process runs and how long
	- preemption is not always needed
	- Goals
		- meeding deadlines
		- predictability


System call numbers
- identifiers of system calls within the system call table

System call handler
- implements the actual service
- what
	- saves registers that it taints
	- reads the parameters that were passed by the caller
	- sanitizes / checks parameters
	- checks if process has permission to perform the requested action
	- performs the requested service on behalf of the process
	- returns to the caller wit ha success or error code

System calls
- functions calls implemented by the OS
- called when User Mode process requires higher privilege
- man 2 syscalls; on linux
- Types
	- Process control
	- memory management
	- file management
	- device management
	- communication
	- information maintenance
	- system management
- Only one system call interface (entry point) into the kernel)


Interrupts
- External device sends signal to the CPU
- Devices use interrupts to signal predefined conditions to the OS
	- device has an "interrupt line to CPU"
- On interrupt
	- CPU looks up the interrupt vector
	- interrupt service routine first saves the state of the interrupted process
		- Instruction pointer
		- Stack poineter
		- Status word
	- transfers control to the respective interrupt service routine in the OS that handles the interrupt
- examples
	- packet from network interface card has been received

Exceptions
- CPU realizes a notable condition.
- An unusual condition makes it impossible for the CPU to continue processing
- on exception
	- CPU immediately stops the process and transfers control to the kernel.
	- Kernel determines the reason for the exception
	- if kernel can resolve the problem (do it and continue)
	- else kill process

Interrupt vs exception
- interrupts can happen in any context
- exceptions always occur synchronous to and in the context of a process or the kernel.


Interrupt vector
- a table, pinned in memory, that contains the addresses of all service routes (set up by the OS)


Interrupt service routine
- handles interrupt

Why system calls?
- We want to protect processes from one another so we restrict them by running them in CPU user mode
- In CPU user mode, processes cannot manage protected resources such as hardware
- So the OS provides services to applications (hardware management)
	- In effect the OS allows the process in user mode to perform privileged operations, but monitors them closely
	- i.e.
		- application calls system the system via syscall
		- OS checks if action is allowed
		- if allowed (and application has not exceeded its quota) the OS performs the action in kernel mode on behalf of the application

Syscalls vs. APIs
- The syscall interface between applications and OS services provides a limited number of well-defined entry points to the kernel
- Programmers often use syscalls via APIs such as printf (implemented with write)


Programmable interrupt controller
- manages interrupts
- interrupts can be masked
	- masked interrupts are queued and delivered when the interrupt is unmasked
	- queue has finite length -> interrupts can geet lost

Timer interrupt
- periodically interrupts processes an switches to kernel (can then switch processes)

APIs
- Win32 API
- POSIX API (UNIX, linux and mac os x)
- C API (man 3)

Memory management unit (MMU)

Preemption
- stop / pause a currently scheduled task in favour of a higher priority task

Threads
- a process consists of 1 or more threads representing execution states
- With more than 1 threads there are also multiple stacks
- A lightweight process (LWP)
	- execution stream that shares an address space
- A function running within the same memory space as other functions, with more than one of them active at a time.

Atomic instruction
- executes all at once

The kernel
- A program at the core of a computer's operating system.
- Generally has complete control over everything in the system
- The portion of the OS code that is always present in memory
- does not always run in the background
- Three occasions invoke the kernel to switch to kernel mode
	- System calls
	- interrupts
	- exceptions

CPU switch
- kernel is responsible for this
- Can switch at any system call (because not always running unless invoked)


Preemptive scheduling
- requires the kernel to be invoked in certain time intervals
- Uses timer interrupt as a trigger to make scheduling decisions (in general)

Yield system call
- currently running process asks kernel to switch to another process

Process list / task list
- list of all ready processes and info about what is currently running
- allows the ability to run multiple programs at once
- also tracks blocked processes
- when an I/O even completes the OS should make sure to wake the correct process and ready it to run againl

what is stored when a process is not running
- register context
	- contents of its registers


Process states
- ready
	- Waiting to be assigned to a processor
- running
	- Instructions are currently being executed
- blocked
	- The process is waiting for some event to occur
	- e.g. IO / device
- initial / new
	- when being created
	- Has been created but was never run
- final / zombie state
	- when exited but not yet cleaned up
	- allows other processes to examine the return code of the process

wait()
- waits for a child process to complete
- returns return code
- indicates to the OS that the child process can be cleaned up


interfaces for process creation and control
- fork
	- creates an almost identical copy
		- returns PID to parent
		- returns 0 to child
- wait
	- wait for child
	- waitpid -> better
	- when the child is finished executing, wait returns its exit code to the parent -> also waits for the child to die (sad :,( )
- exec
	- loads code from its given executable and overwrites its current code segment (and current static data) with it
	- the heap and stack and other parts of the memory space of the program are re-initialized
	- finally the program simply runs that program passing in any arguments as the argv of that process
	- It does not create a new process! (transforms the current process)
- Why this interface?
	- lets the shell run code after the call to fork() but before the call to exec
	- can alter the environment of the aoubt-to-be-run-program

signals
- signal() syscall catches signals


Limited direct execution (LDE)
- Direct execution
	- run the program directly on the CPU
	- very fast -> running directly on hardware
	- but
		- how do we make sure the program doesn't do anything it's not supposed to (while running efficiently)?
		- how do we stop a process (while it is running) and switch to another one.
	- without limits on running programs, the OS wouldn't be in control of anything, and thus would be jsut a library
- protocol 
	- two phases
		- at boot
			- kernel initializes the trap table and the CPU remembers its location for subsequent use -> kernel does so via a privileged instruction
		- when running a process
			- kernel sets up a few things before returning from trap to start the exeuction of the process
			- switch the CPU to user mode and begin running the process
			- when process does system call
			- trap back into OS, which handles it and returns control via a return-from-trap to the process
				- when finishedOS cleans up and we're cool
- low-level mechanisms to implement CPu virtualization
- Just run the program you want on the CPU, but first make sure to set up hardware so as to limit what the porcess can do without OS assistance
- Runs programs efficiently but without loss of OS control
- for the most part, let the program run directly on the hardware; but at certain key points in time (syscall / interrupt) arrange so that the OS gets involved and makes sure the right thing happens
- let the program run efficiently, but make sure the OS maintains control over the hardware

user mode
- code that runs in user mode is restricted in what it can do
- does not have full access to hardware resources
	- system calls
		- special instructions to trap into the kernel and return from trap back to user-mode
	- trap table
		- set up at boot time
		- stores system call numbers
		- finding the trap tables is a privileged instruction
	- trap handlers
		- tells hardware what code to run when certain exceptional events occur
		- e.g. keyboard interrupt, hard-disk interrupt, etc.
- e.g. cannot do IO -> exception
- system calls come in their stead

kernel mode
- code that runs can do what it likes, including privileged operations
- has access to the full resources of the machine
- e.g. issuing IO requests 
- perhaps stores in a single bit of the processor status word


switching processes -> cooperative
- OS trusts the processes of the system to behave reasonably.
- Processes that run for too long are assumed to pereiodically give up the CPU so that the OS ca ndecide to run some other task
- yield() syscall
	- transfers control to the OS so it can run other processes
- Exceptions (e.g. div by zero)
	- trigger trap instruction -> i.e. trigger the OS
- I.e. The os regains control of the CPU by waiting for a system call or an illegal operation of some kind to take place
- but
	- what if infinite loops!


switching processes -> timer interrupt
- A timer device is programmed to raise an interrupt every so many milliseconds. When interrupt is raised, the currently running program is halted, and an interrupt handler in the OS runs
	- The OS now has control.
- at boot the OS 
	- informs hardware of which code to run when timer interrupt occurs
	- starts the timer -> privileged operation
- The OS can feel safe in that control will eventually be returned to it
- the timer can be turned off -> privileged
- responsiblity of hardware when an interrupt occurs
	- save enough of the state of the program that was running when the interrupt occurred, such that a subsequent return-from-trap instruction will be able to resume the running program correctly
	- saved onto a kernel stack
- non-cooperative approach to CPU scheduling


Saving / restoring context -> context switch
- controls the switch between different processes
- save register values for the currently-executing process (onto a per-process kernel stack) and restore a few for the soon-to be exeuctig program
- to save the context of the currently-running process, the OS will execute some low-level assembly to save registers to kernel stack (and kernel stack pointer) and switch to the kernel stack for the next process
	- switching stacks allows the kernel to enter the call as one process, and return  as another
	- return-from-trap starts running the new process



the trap instruction
- when a system call is called, the library uses an agreed-upon calling convention wit hthe kernel to put the arguments to open() in well-known locations, puts the system-call number into a well-known location as well (stack or register) and the nexecutes the trap instruction
- the code in the library unpacks the return values and returns control to the program that issued the syscall
- jumps into kernel and raises the privilege level to kernel
- os then does return from trap -> back to user mode
- save context between
	- registers
		- program counter
		- flags
		- and few others to per-process kernel-stack
- Saves register state carefully, changes the hard-ware status to kernel mode, and jumps into the OS to a pre-specified destination (the trap table)



Scheduling policies
- performance vs. fairness
- list
	- FIFO / FCFC (first in first out / first come first serve)
		- schedule processes in order of arrival
		- convoy effect -> if long process first, response time bad
	- SJF
		- Optimal turnaround (and waiting and response times)
		- Challenges
			- cannot know job lengths in advance
			- CPU bursts interleaved with waiting IO (instead of single continuous computation)
			- Solved with
				- predicting the length of next CPU burst for each process
	- STCF (shortest job to completion first)
		- Preemptive SJF PSJF
		- Preempt periodically to make a new scheduling decision
		- At each time slice
			- schedule job with shortest remaining time
			- Or
				- schedule job whose next CPU burst is the shortest

Scheduling for interactive systems
- Round robin RR
	- Each process runs for a small unit of CPU time
		- time quantum / time slice (usually 10 - 100 milliseconds)
	- Preempt processes that have not blocked by the end of time slice
	- append current thread to end of run queue, run next thread.
	- Thoughs
		- balance interactivity and overhead
			- context switch / dispatching (overhead)
			- The larger the time slice, the smaller the overhead
				- but also less multiprogramming / less fairness
	- Analysis
		- higher average turnaround than SJF but better response time
		- Good average waiting time if job lengths vary
		- unfair for IO-bound jobs
			- block before using up time quantum
			- CPU-bound use their entire quantum
			- with same amount of slices, CPU-bound jobs get more CPU time
			- solution see VRR
- Virtual round robing VRR
	- Put jobs that didn't use up their quantum into an additional queue
		- Store the share of time-slice that they have not used up with the job
		- jobs in the additional queue get priority over other jobs
		- After finishing, put back in normal queue
- Multi-level feedback queue
	- Minimize turnaround time
	- Minimize response time for interactive jobs
	- Gets a good trade-off between interactivity and overhead
	- goals
		- give higher prio to IO-bound jobs
		- give low prio to CPU bound jobs, but run them longer at a time
	- How
		- different queues with different priorities and time slices
			- Run job from non-empty quue with highest priority
			- Becomes RR if multiple jobs are on the same queue
			- Double time slice length in each next-level priority
			- demote processes that repeatedly use up their quantum to lower priority
			- promote processes into higher prio
				- when they don't use up their qquantum repeatedly
				- or all jobs after some time

Priority scheduling
- Not all jobs are equally important
- Associate priority number with each process
	- Allocate CPU RR to processes with highest priority
- Preemptive or non-preemptive
- SJF is priority scheduling where priority is the predicted next burst time
- Strict priority scheduling
	- Processes don't execute if there is always a runnable process with higher prio
		- To solve this weaken strictness in some way

Priority donation
- Process B may wait for result of A, but A has lower prio than B
- Solve with prio donation (priority inheritance)
	- Give A the priority of B as long as B waits for A
- If B,C,D,E wait for A, A only gets highest priority of those

![Screenshot 2024-04-14 at 12.13.56.png](../images/Screenshot%202024-04-14%20at%2012.13.56.png)
Lottery scheduling
- Issue number of lottery tickets to processes
- more tickets -> higher prio
- Amount of tickets controls average proportion of CPU for each process
- draw random number, then finds the owner of that number

Linux CPU scheduler
- Goals
	- fairness
	- low task response time for IO bound / interactive tasks
	- High throughput for CPu bound tasks
	- Low scheduling overhead
	- timeslice based on prio (manually / dynamically adjusted)
	- suitable for multi-CPU / multi-core
		- Efficient and balanced load on multiple CPUs
	- Needs to work in a number of different environments
- modern linux sceduler
	- multiple scheduling policies within scheduling classes
	- task migration between CPUs, policies, and classes
		- generic API for scheduling class
	- runqueues
		- one runqueue set per CPu
			- deadline
			- realtime
			- completely fair shceduler run queues

Scheduling classes
- stop
	- highest priority
	- only used in multiprocessor systems
	- single "migration/N" kernel thread per CPU
	- used for task migration
- Deadline
	- Highest prio after stop
	- based on earliest deadline first scheduling
		- tasks can declare their required runtime and their period of execution
		- taskss are allowed to run during an assigned budget
		- will be suspended after full budget has been used
- Realtime
	- POSIX real-time tasks
	- FIFO or RR with 10 ms default timeslice
- CFS
	- completely fair scheduler
- IDle
	- lowest prio
	- one idle kernel thread per CPU
	- runs only when nothing else is runnable

Multi-CPU scheduling in Linux
- Runqueue per CPu
	- core-local scheduling without cross-core synchronization
	- Core may be idle while other cores have jobs wating in their queues
- load balancing
	- periodically shift load
	- requires exclusive access to run queues


Niceness
- -20 most favorable
- 19 least favorable
	- I.e. if 19 nice -> then let's others run first
	- if -20 nice -> then tries to run as often as possible


CFS -> completely fair scheduler
- tracks virtual runtime (vruntime) of tasks (time on CPU)
- task with shortest vruntime runs first
- Internal data structure
	- red-black tree representing timeline of future task executions
	- insertion based on vruntime
- IO-bound tasks (low vruntime) get higher prio
- CPU-bound jobs don't get more CPU time
- Prio defines wieght of task in vruntime calculation
	- higher weight -> slower vruntime increase
- On scheduler activation
	- advance vruntime fo current process by (weighted) elapsed time
	- pick process with smallest vruntime as next process (using the red-black tree)




Process behavior -> boundedness
- CPU-bound process
	- spends more time doing computations
	- few very long CPU bursts
- IO-bound process
	- spends more time doing IO than computations
	- many short CPU bursts


FIFO first in first out 
- serve the thing that came first
- cons
	- the convoy effect 
	- if a really heavy process comes first, then the turnaround time of all the processes after it get fucked

SJF shortest job first
- The optimal scheduling algorithm -> but needs omniscience (knowing how long each process will run)
- (aaand its technically FIFO if not everything arrives at the same time)

STCF -> shortect time to completion first 
- basically, SJF with preemption PSJF
- every (insert time interval) or when a new operation arrives, reeavluate what is the shortest to run.
- Bad for response time

Round Robin
- instead of running jbos to completion, run a job for a time slice (scheduling quantum) and then switch to next job in the run queue
	- repeat until jobs are finished
	- the time slice must be a multiple of the timer-interrupt period
- Making the time-slice too short is problematic
	- too much time spent context-switching -> the slice needs to be long enough to amortize the cost of switching, but not so long that the system is no longer responsive
	- alos think of CPU caches, TLBs, branch predictors etc. This is a state that needs to be flushed when the currently-running job is brought in
- ONE OF the WORST policies for turnaround time

Preemption
- stopping a process to reevaluate the scheduling situation
- then (maybe) context switch to another process


Scheduling metrics
- performance
	- Turnaround time
		- the time at which the job completes minus the time at which the job arrived in the system
			- tCompletion - tArrival = tTurnaround
			- -> or this formula for everhythig divided by the number of things
	- Response time
		- the time from when the job arrives in a system to the first time it is scheduled
			- tResponse = tFirstrun - tArrival
- Fairness
	- Jain's fairness index
- Tradeoffs
	- fair policies, that evenly divide the CPU among active processes will perform poorly on turnaround time
	- if you're unfair turnaround time is increased, but at the cost of response time
	- fairness lowers resopnse time, but at the cost of turnaround time


Starting a program
- create process entry in process list
- allocate memory for it
- load the program code into memory (from disk)
- locates its entry point (main())
	- jumps to it
- starts running code
- ...
- free memory of process
- remove from process list

time sharing
- share the physical CPU among many jobs running seemingly at the same time


Multi-level feedback queue MLFQ
- a common approach to scheduling
- observes exeuction of a job and prioritizes it accordingly
- purpose
	- optimize turnaround time
	- make a system feel interactive to users
		- minimize response time
- How
	- learn as the system runs, the characteristics of the jobs it is running, and thus make better scheduling decisions
- implementation
	- multiple distinct queues, each assigned a priority level
	- A job that is ready to run is on a single queue
	- use priorities to decide which job to run at a given job
	- Varies the priorities of a job based on observed behavior
		- if a job repeatedly relinquishes the CPU, MLFQ will keep its priority high -> interactive processes
		- if a job uses the CPU intensively for long periods of time, reduce priority -> CPU intensive
	- Use the concept of allotment
		- the amount of time a job can spend at a given priority level before teh scheduler reduces its priority
	- i.e.
		- assume that the new job is a short job
		- if short -> completes quickly anc complete
		- if slow, it will move down queues
- Problems
	- Starvation
		- if there are too many interactive jobs, then the long-running processes will never get the recourses they require
	- Gaming the scheduler
		- A programmer tricks the scheduler into thinking that his program is short
	- dynamic behavior
		- change from long-running IO to interactive
- Fixes
	- after some amount of time, move all jobs to the topmost queue
		- solves for dynamic behavior & starvation
		- time
			- too high -> long-running jobs starve
			- too low  -> interactive jobs don't get proper share of CPU
	- keep track of the time total time spent per level
		- harder to game
	- varying time slice lengths for each queue level
	- Many schedulers reserve the highest priority levels for operating system work

nice
- tell the system what priority level you want for a process

Most systems allow for advice on some level -> nice (scheduling) madvice -> memory managing, informed prefetching and caching -> file systems


Multiprogramming
- running multiple processes at once and the OS switches between them
- letting a process use all the memory, then loading to disk, and picking another process is fucked
- issue
	- protection of resoruces in shared space
- Benefits
	- can run a process while another process is doing IO


Address space
- the running program's view of memory in the system
- Virtualizes memory
	- the running program thinks it is loaded into memory at a particular address (=) and has a potentially very large address space
	- transparent -> invisible to the running program
- Goals of virtual memory
	- transparency
	- efficiency -> time and space
	- protection
		- protect processes from one another as well as the OS itself from other processes
		- a process should not be able to access or affect in any way, the memory contents of any other process or the OS itself (anything outside its address space)
		- isolation -> property
			- each process runs in its own isolated cocoon
- abstracts physical memory 
- what is in the address space
	- Code 
		- static and placed at top of memory
	- heap
		- dynamically-allocated, user-managed memory
		- grows and shrinks
	- stakc
		- keeps track of where it is in the function call chain and allocates local variables and passes parameters and return values to and from routines
		- grows and shrinks



Virtual memory
- ensure that program are able to use their address space in whatever way they would like
- Create the illustion that the program has its own private memory, where its own code and data reside
- Turn the ugly machine reality into a useful, powerful, and easy to use abstraction
- OS controled
	- the OS ensurs that no application is allowed to access any memory but its own, thus to protect applicaiotons from one another, and the OS from applications, we need help from the harware too
- We would like 


Address translation
- transforming a virtual address into a physical address
- The OS can control each and every memory access from a process, ensuring the accesses stay within the bounds of the addres space
- needs hardware support to be efficient


hardware-based address translation -> address translation
- the hardware transforms each memory access, changing the virtual address provided by the instruction to a physical address where the desired information is actually located
- performed on every memory reference
- OS must manage memory
	- keep track of 
		- free
		- used memory
- Problem
	- relocate the process in memory, in a way that is transparent to the process
- Types
	- based and bounds / dynamic relocation
	- Segmentation

Static relocation
- loader takes an executable and adds the offset within physical memory to every memory reference
- no protection -> not smart


base and bounds / dynamic relocation
- Need two hardware registers within each CPU (MMU)
	- base
		- the physical address at which the process' memory actually starts
	- bounds (limit)
		- the limit of that address space
- virtual address
	- physical address = virtual address + base
- Dynamic relocation is possible
	- Can move the address space of the process, even after the process has strated running 
- Needs privileged instructions
	- modify the base and bounds registers (done by kernel)
	- handlers for exceptions 
		- out of bounds
		- user tries to change base and bounds himself
- on context switch
	- OS saves registers to PCB
- Hardware handles address translation without the involvement of the OS
- Issues
	- internal fragmentation -> too much space allocated
		- space between stack and heap
	- Very hard to make address space bigger if we need to 
		- practically limited to the size we allocated at first.


Segmentation / generalized base / bounds
- instead of having just one base and bounds pair in our MMU, why not have a base and bounds pair per logical segment of the address space
- segment
	- a contiguous portion of the address space of a particular length
- allows the OS to place each of the process' segments into different parts of physical memory
	- f.x. each of the code, stack and heap
- why
	- less internal fragmentation
	- allows for a sparse address space
		- where only part of the address space is allocated some memory
- Implementation
	- three base and bounds pairs
		- code
		- heap 
		- stack
- can implement code sharing
	- mark code segment as read-execute, other segments as read-write (protection bits)
	- Allows same physical segment to be shared between active process'
- fine-grained
	- more segments per process in smaller chunks
	- requires a segment table
		- enables a syste m to use segments in more flexible ways
- translation
	- address in heap
	- extract the offset into the heap
		- add vaddress to the base of the code
		- or vaddress - (segAddress - codeBaseAddress) + segAddress
	- how to find the correct segment
		- Top two bits are the segment
		- bottom 12 bits are offset into the segment
	- issues
		- can only be of specific size (segments (top x bits) can only refer to x amount of memory)
		- Needs to know of segment grows in positive or negative direction
		- SKOÐA negative direction
- OS problems
	- what should happen on context switch
		- the segment registers must be saved and restored
	- when segments need to grow (for mor space) (or shrinks)
		- call sbrk to grow the heap
		- update segment size register
	- Manage free space in memory
		- might become full of holes after some time (external fragmentation)
		- holes not big enough to actually house a whole segment, but still unused free space
		- new segment too large
		- or not enough space available to grow a segment directly
	- Compaction
		- rearrange existing segments such as to minimize external fragmentation
		- memory intensive to copy the esgments
		- uses a lot of CPU time
		- Also makes requests to grow existing memory harder to serve
	- Other than compaction
		- use a free-list strategy that tries to keep large extents of memory available for allocation
			- best-fit
				- keeps a list of free spaces and returns the one closest in size that satisfies the desired allocation 
			- worst-fit
			- first--fit
			- buddy aglrotihm
		- External fragmentation will always exist, so a good algorithm just tries to minimize it
- Benefits
	- dynamic relocation
	- support for sparse address spaces
	- fast -> arithmetic for segmentation is easy
	- code-sharing
- cons
	- Variable sized segments are hard to manage -> external fragmentation
	- segmentation is not flexible enough to support fully generalized, sparse addresss spaces
	- if we have a large but sparsely-used heap in one logical segment, the entire heap must still reside in memory in order to be accessed


Free space management
- easy when the space you are amanging is divided into fixed-sized units
- minimizing external fragmentation
- uses some kind of free list
	containing references to all the free chunks of space in the managed region of memory
- No compaction of free space is possible
	- Since a heap gives out pointers, and those pointers can't really be found and updated
- Common mechanisms
	- splitting
		- Find a free chunk of memory and split it in two
			- 1 a chunk containing the newly allocated memory
			- 2 a chunk containing the rest of that space
	- coalescing
		- When space is freed, if there is free space either to the left or right of it, then this space is compacted into one entry
- how
	- header for each segement
		- size of segment
		- magic
			- Check magic to make sure that the memory you're in actually points to a free block in memory
		- Actual data
	- the size of the header is equal to the size requested + the size of the header.
		- Thus when looking for space in memory you must look for space that can fit both the size requested and the header itself.
	- The list is built in the free space itself
- How initialized
	- Call mmap() to get free space of some specific size
	- create one entry with header, and size heapsize - headersize
- How to grow
	- sbrk called
		- OS finds free physical pages, maps thme into the address space of the requesting process, and returns the value of the end of the new heap
- management strategies (which block to take?)
	- best fit (smallest fit)
		- Search through the entire free list, and find chunks of free memory that are as big or bigger than the requestd size, then return the opne that is smallest in that group of candidates
		- intensive -> searching through the ENTIRE free list
	- worst fit
		- Find the largest free chunk, and return the requested amount
		- tries to leave large chunks free
		- bad -> leads to excess fragmentation and has a high overhead
	- first fit
		- finds the first block that is big enough and returns the rewquested amount to the user
		- speedy -> no exhaustive search
		- sometimes pollutes the beginning of the list with small object
		- thus how the allocater manages the lists order becomes an issue
		- using address-based ordering
			- keep the list ordered by the address of the free space
			- coalescing becomes easier and fragmentation tends to be reduced.
	- Next fit
		- keep extra pointer to the location within the list where one was looking last
		- spread the seraches for free space throughout the list more uniformly
		- avoids splintering at the beginning of the list


Segregated lists (free list
- if a particular application has one or a few popular-sized request that it makes, keep a separate list just to manage objects of that size, all other requests are forwared to a more general memory allocator.
- the slab allocator)
	- allocate a number of object caches for kernel objects at boot up
		- (locks, file-system inodes, etc.)
	- each object cache is a segregated list
	- The general allocator can reclaim the mfrom the specialized allocator, which is often done when the VM system needs more memory


the mmap() system call
- returns a pointer to free space in physical memory


Buddy allocation
- the binary buddy allocator
- free memory is thought of as one big space of size 2^n
	- all contiguous allocated / free memory chunks have fixed power of 2 size
	- all chunks are naturally aligned
- requests rounded up to the next higher power of 2
	- internal fragmentation, but way less external fragmentation
- Used to dynamically allocate contiguous chunks of fixed-size segments
	- if no sufficently small memory block is available
		- select larger chnk and split it into two unti lappropriately sized chunk is available
	- if two buddies are bot hfree
		- merge buddies to larger chunk
		- the address of each buddy block differes by a single bitto  (easy to find)


Other advanced allocators
- searching is generally slow
- use new data structures to search
	- balanced binary trees
	- splay trees
	- partially-ordered trees


Paging
- chopping the physical memory into fixed-sized pieces
- Divide the address space into fixed-sized units each called a page
- Physical memory
	- viewed as an array of fixed-sized slots called page frames. Each of these frames can contain a single virtual-memory page
- OS keeps page table (per-process)
	- records where each virtual page of the address space is placed in phyiscal memory
	- stores address translations for each of the virtual pages of the address space
	- i.e. says where each page is stored in physical memory
	- per-process
		- because similar virtual addresses map to different physical addressees between processes
- Virtual address translation
	- Split into two components
		- virtual page number (VPN)  (high order bits)
			- used in page table to find the PFN
				- physical frame number (PPN physical page number)
		- offset                     (low order bits (LSB))
			- which byte within the page we want.
- Benefits
	- flexibility
		- supports the abstraction of an address space effectively, regardless of how a process uses the address space
		- won't make assumptions about the directions that heap and stack grow, and how they are used
	- Simplicity of free-space management
	- No external fragmentation
- Fuck
	- can be too big
	- can slow things down
		- system translates vaddress to paddress
			- fetch proper page table entry
			- perform translation
			- load data from pmem
		- must know where page table is
			- page-table base register
		- fetch PTE from memory, extract PFN and concatenate to offset
		- i.e. one extra memory reference, per memory reference.

Page tables
- stores virtual-to-physical address translations for pages
- A data structure that is used to map virtual addresses (VPN) to physical addresses (PFN)
- records on a per-process basis, where each virtual page of the address space is placed in physical memory
- page tables can get quite large (far more than the two base/bounds register f.x.)
- where are page tables stored?
	- Too big to store on MMU (on-chip hardware)
	- must use memory of some kind
	- Can be stored in OS virtual memory, or even on disk
- Bits / state
	- valid bit
		- indicates whether a particular translation is valid
		- i.e. marks addresses that are not allocated.
		- important to support sparse address spaces
		- i.e. we don't need to allocate physical page frames to those pages.
	- Protection bits
		- indicating permissions
			- read
			- write
			- execute
	- Present bit
		- indicates whether this page is in physical memory or on disk (has been swapped out)
		- to support address spaces that are larger than physical memory
			- page replacement
	- accessed bit
	- dirty bit
	- abstract actual bits
		- present bit
		- read/write bit
		- user/supervisor bit
		- bits to determine how hardware caching works for these pages
		- accessed bit
		- direty bit
- Types
	- linear page table
	- 



![Screenshot 2024-04-15 at 16.53.15.png](../images/Screenshot%202024-04-15%20at%2016.53.15.png)
![Screenshot 2024-04-15 at 16.53.32.png](../images/Screenshot%202024-04-15%20at%2016.53.32.png)




Calculating page table sizes
- VPN
	- an n bit VPN implies that there are 2^N translations that the OS would have to manage for each process 
- PTE - page table entry
	- 4 - 8 bytes generally
- size of page table
	- 2^VPNsize * PTEsize

Inverted page tables
- are not per-process
- an extreme space saving method
- one page table that has an entry for each physical page of the system
- each entry tells us which process is using this page, and which virtual apge of that process maps to this physical page.
- finding the correct entry usess search
- often uses a hash table

Linear page table
- an array of pages
- Index the array by VPN and looks up the PTE at that index, in order to find PFN


MMU -> memory management Unit
- a part of the processor that helps with address translation
- Provides
	- architectural support to achieve safe and secure protection
- hardware device maps virtual to physical address
- I.e. MMU controls the logic behind the virtual address space in hardware.

Free list
- Simply a list of the ranges of physical memory which are not in use
- Used by the OS to keep track of memory that is not in use

allocating physical memory to a process
- First the OS must take action when a process is created, finding space for its address space in memory
- When proces sis terminated
	- OS reclaims memory for use in other processes
	- put memory back on free list
	- clean up associated data structures



TLBs  translation-lookaside buffer
- a cache that stores recent memory translations
- faster address translation
	- using small, fast on-chip memory
- Hardware to speed up address translation
	- part of the MMU
	- a hardware cache of popular virtual-to-physical address translations
	- a sort of address-translation cache
- how
	- on virtual memory reference (load / store), check TLB to see if translation is already there
		- very quick as many TLB entries can be compared in parallel
	- if so -> perform translation quick, without page table
	- Typically there's a 95 - 99% hit rate
- Algorithm
	- extract VPN form vaddress
	- check if TLB holds the translation for this VPN
		- if true
			- TLB hit
			- Use PFN right away, add offset to create paddress
		- else
			- TLB miss
			- Fuck!
			- find PTE in page table (mem access)
			- update TLB with translation
			- retry
				- now perform true
- Handling TLB misses
	- hardware managed TLBs
		- old -> always hardware handling TLB misses (CISC complex instruction set computers)
		- hardware has to know where page tables are located in memory (page table base register) and exact format
		- Evict a TLB entry based on a policy encoded in hardware without involving the OS
	- Software managed TLBs
		- RISC (reduced-instruciton set computers) 
		- on miss, hardware raises an exception, which pauses the instruction stream, raises privilege level to kernel mode, and jumps to a trap handler
			- OS receives TLB miss exception
			- decides which entry to evict form TLB
		- Code in OS searches the page table and uses privileged instructions to update the TLB and returns from trap
		- return-from-trap
			- Usually jump to instruction after
			- on TLB miss, jump to same instruction (that caused the TRAP / exception)
		- Don't cause an infinite chain of TLB misses
			- keep TLB miss handlers in physical memory (not subject to address translation)
			- reserve some entries in the TLB for permanently-valid-translations and use some of those for the handler code itself
				- wired translations that always hit.
		- Why
			- flexible
				- OS can use any data structure for page table without hardware change
			- simplicity
				- hardware doesn't do anything, just the software
				- simple exception then retry
- paging requires a lot of mapping information
	- generally stored in phsyical memory
	- using paging requires one extra memory lookup for each virtual address generated by the  program.
- Benefits
	- speed up paging, making virtual memory possbile
	- Improves performance when spatial locality is there
		- data is packed tightly (references fewer pages / same pages often)
	- same for temporal locality
		- reference same pages in some time interval
- When is TLB bad
	- Exceeding the TLB coverage
		- if number of pages a program accesses in a short period of time exceeds the number of pages that fit into the TLB, the program will generate a large nujmber of TLB misses and run quite slowly.
		- how to fix
			- larger page sizes
				- effective coverage of the TLB increased
	- Program structure can have impact on TLB effectiveness

TLB hardware insides
- 32, 64, or 128 entries
- fully associative
	- no ordering, any translation can be anywhere in the TLB
	- hardware seraches the TLB in parallel to find the desired translation
- TLB entry
	- VPN | PFN | other bits (for each entry)
	- other bits
		- valid bit -> entry is a valid translation
	- protection bits
		- read, write, execute
	- address space identifier ASID
		- results in less TLB misses
	- dirty bit
		- written when a page has been written to
		- used for caching the page's contents in memory

TLB & context switching
- each address translation is only valid for one process (the currently running process)
- how to fix
	- flushing
		- empty the TLB by marking everything with the invalid bit
		- software-based -> a privileged hardware instruction
		- hardware-managed -> enacted when page-table register is changed
		- Can be costly (as there are fewer hits)
	- hardware support to share TLB across context switches
		- address space identifier (ASID) (PID but in the TLB)
		- only a few bits (8 maybe)
		- must set register to for hardware to see which process is active

TLB cache replacement
- when installing a new entry in the TLB, we have to replace an old one
- Policies (examples)
	- LRU -> least recently used
		- evict the one that was least recently used
		- takes advantage of locality in the memory-reference stream
		- Can be gamed
			- program loops over n + 1 pages with a TLB size of n (everything is a TLB miss)
	- Random
		- exactly what it says
		- extremely fast and simple
		- No way to game this (not situation where this is always bad)

TLB reach / coverage
- the amount of memory accesible with TLB hits
	- TLB reach = TLB size * page size


Valid bits oin TLB vs. page table
- page table --> PTE is not mapped
- TLB        --> address is no longer valid
	- initial state
	- context switch.

TLB entry (example)
- may contain
	- VPN
	- PFN
	- G -> global bit, set if shared globally for processes
	- ASID -> some bits that indicate the process that owns the address
	- C -> coherence bits, determin ho page cached by hardware
	- dirty bit -> marked when written to
	- valid bit -> valid / invalid
	- (opt) page maks field
		- for supporting pages of different sizes.
- How many entries
	- often 32- 64
		- a few may be reserved for the OS
		- wired registers
			- tells the TLB how many slots of the TLB to reserve for the OS
				- for entries that would be bad to have TLB misses in

TLB example instructions
- TLBP -> probe to see if translation exists
- TLBR -> read contents of specific TLB entry
- TLBWR -> replace random TLB entry
- TLBWI -> replaces a specified TLB entry


RISC and CISC
- RISC
	- few instruction primitives that the compiler can use
- CISC
	- a lot of instruction, each relatively powerful
- with time became quite similar
- both usable today


Reducing page table sizes
- solutions
	- Just use bigger pages
		- smaller page tables
		- Far more internal fragmentation
	- Have multiple page sizes
		- Doesn't actually solve the problem in and of itself
		- Buut, reduces pressure on the TLB
	- paging with segmentation
		- one page per logical segment
		- e.g. three pages
			- code
			- heap
			- stack
		- base and bounds
			- Hold physical address of the page table of that segment
			- bounds -> how many valid pages?
			- invalid pages don't take space in the page table
		- issues
			- still using base and bounds
			- less flexibility
			- still wasteful if sparse heap
	- Multi-level page tables
		- see chapter

Multi-level page tables (using multi-level indexing)
- turn linear pages into trees
- how
	- chop the page table into page sized units
	- if an entire page of PTEs is invalid, don't allocate that page of the table at all
	- page directory
		- track whether a page of the page table is valid
		- tell where a page is or if ethe entire page of the page table contains no valid pages.
- benefits
	- allocates page-table space in proportion to the amount of address space you are using
		- compact and supports sparse address spaces
	- if carefully constructed, each portion of the page table fits neatly within a page
		- easier to manage memory
		- OS can grab next free page, when it needs to allocate or grow a page table
	- page tables can be placed anywhere in memory
		- and their (potentially) huge size doesn't have to lay contiguously in memory
- more than two levels
	- more memory accesses!
	- tradeoffs
		- time & space
- Costs
	- TLB miss requires more memory accesses to fix
	- complexity
		- more complex than a linear page-table lookup on a TLB miss
		- page table lookups are more complicated in order to save memory




swapping the page tables to disk
- some system place page tables in kernel virtual memory
	- allow system to swap some of these page tables to disk when memory pressure gets a little tight

Page table calculations
- offset
	- = log2(pageSize)
- VPN
	- = vaddressSize - offset
- PTE per page
	- = pageSize / PTEsize
- Total size a page table can address
	- = PDsize * PTsize * pageSize
- significant bits per level
	- = log2(PTE per page)
- rifja upp kringum bls. 238!!


Memory overlays
- a non-transparent method of allowing memory larger than actual physical memory.
- Managed by the programmers themselves


swap space
- allows the OS to support the illustion of a large virutal memory for multiple concurrently runnning processes
- Using larger, lsower devices to transparently provide the illustion of a large virtual address space
- why
	- multiprogramming -> keeping the memory of all those processes
- how 
	- swap-space -> reserve space on disk for moving pages back and forth
	- assume that the OS can read from and write to the swap space in page-sized units
	- size of swap space determines how many pages can be in use in a system at a given time
	- OS needs to
		- remember disk address of a given page
- Example
	- running a binary file (not actually from swap space)
		- code stored on disk
		- code pages initially found on disk, then loaded into memory
			- all at once
			- or as needed (in modern system)
		- if system needs to make room in physical memory for other needs, it can safely re-use the memory space for these code pages, knowing that it can later swap them in again


Present bit in PTE
- whether page is present in physical memory
- if zero, the page is not in memory, but somewhere on disk
	- page fault -> accessing a page that is not in physical memory
	- page fault handler


Page faults
- Access to a page that is currently not present in main memory
- have a large impact on EAT
- if a page is not present, the OS is put in charge to handle the page fault
	- doesn't matter if TLB is software or hardware managed
- how does the OS find pages on disk
	- page table
		- use PFN for disk addressing
		- look in PTE to find the address, and issues a request to disk to fetch the page into memory
		- then 
			- updates PTE to maker page as present
			- update PFN tto record in-memory location of the fetched page
			- retry the instruction
		- Then
			- maybe a TLB miss
			- run TLB miss handler
- OS needs to 
	- check validity of access
	- get empty frame (free or victim)
		- save / clear victtim
			- dorop if fetched from disk and clean
			- write back modifications if fro mdisk and dirty
			- write pagefile / swap partition otherwise
		- Unmap page from old AS
			- unset valid bit in PTE
			- flush TLB
		- prepare new page
			- NULL page
			- load new contents
		- Map page frame into new address space (S)
			- setvalid bit in PTE
			- flush TLB
	- prepare requested page -> clean or load content from disk int oframe
	- adapt page table -> change some bits
	- set present bit of respective entry
	- restart instruction that caused the page fault
- why software handles this
	- because hardware would have to know too much (how to do IO, and understand swap spaces)
	- because the extra time taken to run software isn't much when compared to the enourmous cost of doing IO
- If memory is full
	- page out! throw some other page out of memory, and onto disk
- how to swap
	- page fault!
	- find free page in memory
	- if none free, page replace
	- read page from disk to free page
	- update page table
	- retry instruction
	- TLB miss
	- load to TLB
	- retry instruction
	- TLB hit

Swapping pages
- pre-fetch surrounding pages
	- reading more block is approximately as fast as reading just the one
	- if application exhibits spatial locality -> cool
- pre-zero pages
	- we don't want to leak info between processes
	- can keep zero in demand (pre-cleaning) (page buffering)
		- pool of 0 pages that is filled in the background when the CPU is idle
		- run a daemon that cleans (writes back changes), reclaims (unmaps), and scrubs (zeroes out) pages for the free pool in the background
		- Smooths IO and speeds up paging significantly



%CR2 -> faulting virtual address

Effective access time
- time to access some page entry



What happens when a program fetches some data from memory
- three important cases for TLB misses
	- page present and valid -> grab from page table, retry fetch
	- valid and not present  -> load from swap, retry fetch, load into TLB, retry fetch
	- not valid and ?        -> raise exception, KILL PROCESS! (or similar)



Why background takss
- allow for grouping of operations (like IO), increased efficiency
	- buffering file writes
	- page daemon


Cache management
- Maximizing cache hits and minimizing cache misses
- Average memory access time (AMAT)
	- AMAT = Tm + (Tmiss * TD)
		- Tm -> cost of accessing memory
		- TD -> cost of accessing disk
		- PMiss -> the probability of not finding the data in the cache
- Types of cache misses
	- cold-start miss / compulsory miss
		- Initial misses (from empty cache)
	- Capacity miss
		- occurs because the cache ran out of space 
	- Conflict miss
		- arises in hardware because of limits on where an item can be placed in hardware cache
		- set associativity
			- does not arise in the OS page cache because such caches are always fully-associative
		- i.e. only happens when there are restrictions on where items can be placed.


page-replacement policies
- Choosing a page to throw into swap space
- throwing the wrong page out is catastrophic! (making the computer run 10.000 - 100.000 times slower)
- how page replacements work
	- OS tries to keep som amount of memory free
	- has high water mark HW and low watermark LW
	- when the OS sees that there are fewer than LW pages available, run page daemon (swap daemon)
		- a background thread that freees memory
		- evicts pagse until there are HW pages available
		- perform a number of replacements at once
			- allows clustering / grouping of pages and writes them out at once to swap partition
			- reduces seek and rotational overheads of a disk - increases performance
- strategies
	- Optimal replacement
	- FIFO
	- LRU
	- Clock algorithm - Approximate LRU
	- LFU
	- RANDOM

Optimal replacement policy
- replace the page that will be access furthest in the future
- fewest number of misses overall
- requires omniscience
- Not really possible in practice, except for extremely simple programs
- great for measuring against


FIFO  - first in first out
- pages placed in queue
- when a replacement occurs, the page on the tail of the queue is evicted
- benefits
	- extremely simple
- cons
	- can't determine the importance of blocks
	- Belady's anomaly
		- a larger cache can cause more cache misses

stack-property of replacement policies
- a cache hit rate will either stay the same or improve as the cache size increases
- FIFO and Random don't have this property!

Random replacement
- pick a random page to replace under memory pressure
- Properties similar to FIFO
- benefits
	- simple to implement
- cons
	- depends on luck

LRU - least recently used
- using historical information to pick a better replacement
	- use frequency. if a page has been accessed many times, perhaps it should not be replaced right away, as it probably has some value
	- Use recency -> actual LRU
		- the more recently a page has been accessed, the more likely it is to be accessed again (temporal locality)
- Implementations
	- Cycle counter implementation
		- Have MMu write CPU's time stamp counter to PTE on every access
		- on page fault, scan all PTEs to find oldest counter value
		- benefits
			- cheap at access if done in hardware
		- cons 
			- memory traffic for scanning
	- Stack implementation
		- Keep a doubly linked list of all page frames
		- move each referenced page to tail of list
		- benefits
			- can find replacement victim in O(1)
		- cons
			- need to change 6 pointers at every access

LFU
- least frequently used

properties of replacement policiies
- if random
	- all policies do the same (except optimal)
- no matter what policy you use, all policies converge to a 100% hit rate when all referenced blocks fit in cache
- 80-20 workload
	- 80% of references are made to 20% of pages
	- LRU has about 80% hit rate at 40% cache size
- sequential access larger than cache size
	- random does best because no corner cases!
	- LRU and FIFO are fucked!

Implementation of historical algorithms
- needs some work at every cache hit and miss!
	- as opposed to FIFO which is only activated on miss
- Scanning all the pages in cache is fucking hard!
	- and having to set a time for every page
- solution
	- Approximating LRU
		- have use bit -> reference bit
		- whenever a page is referenced, the use bit is set by hardware to 1
		- hardware never clears the bit (OS does that)
		- Clock algorithm


Clock algorithm
- approximating LRU with a use bit -> a reference bit set by the hardware
- Imagine all the pages of the system arranged in a circular list
	- A clock hand points to some particular page to begin with
	- when a replacement must occur
	- OS checks if currently-pointed to page P has a use bit of 1 or 0
		- if 1 , page was recently used, and is set to 0, then the clock hand goes 0onto the next page and repeats
		- if 0
			- page has not been referenced recently, or worst case, we've gone around the entire circle
- Also consider dirty pages
	- it's beneficial to not throw out dirty pages right away if possible
		- dirty pages are pages with data written to them, that then need to be written to disk (has not been done yet)
		- so evicting this page, necessitates a write to disk.


Page selction policy
- For most cases, use demand paging
	- bring page into memory when accessed / on demnad
- prefetching
	- guess that a page is going to be used and fetch it ahead of time
	- should only be done when there is reasonable chance of success
	- e.g. if code page 1 is brought into memory, then code page 2 will likely be useful as well.

Clustering or grouping
- when the OS tries to write multiple pages at once to memory
- Disk drives are faster at performing a single write than multiple ones.


Thrashing
- What should the OS do when memory is oversubscribed and the memory demands of the set of running processes simply exceeds the available physical memory
	- constant paging -> thrashing
- How to handle
	- admission control
		- given a set of processes, a system could decide not to run a subset of processes, with the hope that the reduced set of process' working sets fit in memory, and can make progress
		- "it's better to do less work well than try to do everything at once poorly"
- out-of-memory killer
	- when memory oversubscribed, an out-of-memory killer becomes active
		- a daemon that chooses a memory intensive process and kills it
		- successful, but has problems
- System is busy swapping pages in and out
	- each time one page is brought in another page, whose contents will soon be referenced is thrown out
	- reasons
		- memory too small to hold hot memory of a single process
		- access pattern has no temporal locality
			- process doesn't follow pareto principle (past != future)
		- each process fits individually, but too many for system
			- degree of multiprogramming too high
		- page replacement policy doesn't work well
- Linux approach to avoid thrashing
	- the swap daemon
	- separately for file-backed and anonymous pages
		- all pages are on either (not both) list
			- Active list
				- if referenced, move to top of list, otherwise move to inactive list
			- inactive list
				- promote page to active if referenced
				- select eviction candidate from tail of list


Scan resistance
- algorithms that are LRU-like, but also try to avoid the worst-case behavior of LRU (looping-sequential workload)
- a page replacement policy


Synonyms
- aliases
- arises when same data is accessible via several distinct addresses
- only occurs in virtually indexed caches
- multiple virtual addresses can refer to the same physical memory
- bad
	- reduce the effective size of the cache
	- cause coherence issues
		- two forms
			- same data can reside in more than once cache line
				- future reads may require that future reads see the mots recently updated copy of the data
			- coherence of cahce and main memory
				- may require most recently updated copy to be written back to main memory, while all other copies are invalidated to ensure they do not corrupt valid main memory
	- a single piece of data can reside in multiple cache entries
	- Increase in capacity misses

Homonyms
- an address, used in different contexts, which refers to different data
- unique to virtually indexed virtually tagged caches
- when same virtual address is being used in different address spaces, where the virtual-to-physical translations differ

Cache indexing and tagging
- pertains to data and instruction caches of a processor
- Physically-indexed, physically tagged caches
	- physical cache
	- traiditionally favored by processor designers, avoids the problem of synonyms and homonyms
	- Performance limitations
	- two configurations
		- 1 sequential lookup
			- TLB used to obtain physical address
				- then used to index cache
			- problems
				- limits processor's clock speed or requires the TLB and caches to be placed in separate pipeline stages
				- more penalties for exceptions and mispredicted branches
		- 2 parallel lookup
			- TLB and a physical cache can be indexed in parallel
			- removes speed or pipeline penalties
			- only the untranslated offset bits of the virtual address can be used in the index
			- PFN is then copmared to the physical address tag to validate the access
			- cache is limited by W X P
				- W -> associativity of cache
				- P -> the min page size of processor core
- Virtually indexed physically tagged
	- popular in modern processors
	- favoured for large, fast, first-level caches
	- V/P cache and TLB lookup can occur in parallel
	- since index is virtual, size of cache is not limited
	- Subject to synonym problem
		- coherence problems
			- mapping coherence
				- when mapping modified, the p tag of cache lines covered by the modified mapping becomes stale
				- old physical frame may be reused at different virtual address, if a stale cache ntry is written back to main memory it will overwrite the valid data in the reused frame
				- only issue for write-back caches
		- reduce effective size of cache
- PHysically indexed, virtually tagged
	- overcomes size limitations of physical cache
	- uses translation cache known as TLB slice
	- the majority of cache's indices are made up of untranslated offset bits
	- since the cache is tagged with the virtual address, a hit can be detected without translating the complete virtual address
	- TLB slice can be direct-mapped and avoid a validation tag, if the entry is incorrect, the cache's virtual tag mismatch will indicate a miss
	- drawbacks
		- potentially low hit rate of TLB slice
		- increased complexity of a cache miss
			- two possibilities
				- TLB slice miss
					- TLB slice contains incorrect parital translation
					- to validate, the full TLB is queriied on a cache miss to provide the full translation
					- if slice entry ismismatched, it is updated and the access retried
				- virtual tag miss
					- TLB slice contains correct partial translation, but the cache's vritual tag is missed
					- real cache miss or synonym
					- cache also contains a paddress tag, which is then compared with the full tranlsation from the TLB,
						- match hit
						- otherwise no match
			- Use as second level cache shielded by a virtual frist level cache to solve problems
			- weakness
				- faiilure to address issue of how protecction is implemented

Virtually indexed, virtually tagged
- allow both the indexing and tag comparison of the cache to be completely independent of the TLB
- TLB lookups are only needed to validate access permissions of the cache referencing on a hit
- remove the translation step is possible


----


Concurrency


Thread
- an abstraction for a single running process
- An abstraction for execution states of an address space
- multi-threaded programs
	- more than one point of execution
		- multiple program counters
	- multiple stacks -> thread local storage
- Each thread is like a separate process, but they share the same address space, and can access the same data
- in general we view threads as entities created by the priogrammer but scheduled by the OS, in any fashion that the OS chooses
	- locks give the programmer more control of what happnes
- State (each thread has)
	- a program counter
		- tracks where the program is fetching instructions from
		- own private set of registers it used for computatino
	- Requires context switch to change betwen (even if technically in same process)
		- state is changed, but not the address space
	- Thread control block TCB
		- like PCB but for threads
		- stores state of each thread of a process
- Reasons
	- parallelism -> utilize multiple cores
	- Avoid blocking program progress due to slow IO
		- write a program that performs different tyeps of IO
		- instead of waiting, your program may wish to do something else
		- let program do something while waiting
		- overlap of activities with IO within a single program
		- Could use multiple processes, but sharing the same address space is nice in many senarions
- Problems
	- Context switches at effectively random intervals can cause non-determinism (if we're not careful)

Common concurrency issues
- race condition (data race)
	- the results depend on the timing of the code's execution
	- results in indeterminate results instead of deterministic
	- if multiple threads of execution enter the critical section at roughly the same time; both attempt to update the shared data structure, leading to a surprising outcome
- Waiting for access to critical section
	- holding a lock while waiting for IO


Indeterminate program
- consists of one or more race conditions
- output of the program varies from run to run, depending on which threads ran when. 
- outcome is non-deterministic, we usually expect computer programs to be deterministic.

Critical section
- if multiple threads exeucting this code concurrently can sause an issue
- a piecee of code that accesses a shared variable (or resource) and must not be concurrently executed by more than one thread
- Piece of code that accesses a shared resource, usually a variable or data structure
- desired properties of solving critical sections
	- mutual exclusion
		- at most one thread can be in the CS at any time
	- progress
		- no thread running outside of the CS may block another thread from getting in
			- if no thread is in the CS, a thread trying to enter will eventually get in
			- if no thread can enter CS -> no progress
	- bounded waiting / fairness
		- once a thread starts trying to enter the CS, there is a bound on the nubmer of times other threads get in -> no starvation
	- performance
		- time overhead added by using the lock for different cases of no/low/high contention

Mutual exclusion
- guarantees that if one thread is executing within the cricital section, others will be prevented from doing so.
- primitives
	- guarrantees that only a single thread ever enters a critical section, avoiding races, and resulting in a deterministic program outpus

Atomic operations
- "All or nothing" or as a unit
- should appear as if all the actions you wish to group together occurred, or that none of them occurred, with no in-between state occurring.
- sometimes called a transaction


the general set of Synchronization primitives
- hardware instructions with OS support


dup2 ( pipefd [ WRITE END ] , STDOUT FILENO ) ; // Close stdout and replace with fileend

OS and synchronization
- THE os was the first concurrent program
- many techniques were created for use within the OS
- an untimely interrupt is the source of all (most) concurrency issues


Pthreads
- Posix API for thread management and synchronization
- basics
	- A Pthread is associated with
		- an identifer thread id -> TID
		- a set of registers IP and SP (instruction and stack pointers)
		- a stack area to hold the execution state of that thread
	- Pthread_create -> crates a new thread
	- Pthread_exit -> terminate the calling thread
	- Pthread_join -> wait for a thread to copmlete
		- can pass pointer for exit code
	- Phtread_yield
		- release the CPU to let another thread run


creating a thread
- \# include \<pthread.h>
- int pthread_create(pthread_t \*thread, const pthread_attr_t \*attr, void \*(\*start_routine)(void*), void \*arg);
	- thread
		- poitner to a structure of type ptthread_t
		- used to interact with the thread
		- pthread_create initializes it
	- attr
		- attributes this thread might have
		- setting stack size
		- ifo about scheduling policy
		- attribute initialized separately with pthread_attr_init();
		- NULL most of the time
	- start_routine
		- function pointer
	- arg
- Wait for thread
	- int pthread_join(pthread_t thread, void \*\*value_ptr)
	- value_ptr is a pointer to the return value you expect to get back
	- NULL if we don't care about the return
	- DON'T return a pointer to anything on the threads stack!

joining
- using parallelization to do stuff quicker -> yes
- using concurrency to do many things -> no (e.g. web server)

Creating mutex
- int pthread_mutex_lock(pthread_mutex_t \*mutex)
- int pthread_mutex_unlock(pthread_mutx_t \*mutex);
- locks for critical sections
- initializing locks
	- pthread_mutex_t lock = PTHREAD_MUTEX_INITIALIZER
	- sets lock to default and makes usable
	- dynamic lock initialization is done 
		- int rc = pthread_mutex_init(&lock, NULL)
		- assert (rc == 0);
- delete
	- pthread_mutex_destroy
- other
	- trylock
		- fails if lock is already held
	- timedlock
		- returns after a timeout or after acquiring the lock, whichever happens first

Condition variables
- a queue of waiting threads
- always used in conjunction with a mutex
- used to signal threads when state changes
	- if state is already as needed, the thread doesn't wait for a signal
- useful when some kind of signaling must take place betwen threads
	- pthread_cond_t cond = PTHREAD_COND_INITIALIZER
	- int_pthread_cond_wait(pthread_cond_t \*cond, pthread_mutex_t \*mutex)
		- puts calling thread to sleep, and waits for some other thread to signal it
			- usually when something in the program has changed that now-sleeping thread might care about
		- releases the held lock, then reacquires it once woken
		- in while loop because some threads can wake other threads spuriously
	- int pthread_cond_signal(pthread_cond_t \*cond)
		- needs to hold same lock as other, releases, then reacquires
	- to use a condition variable, one has to in additiona have a lock that is associated with this condition
	- when calling either of the above routines the lock should be held
- Always use condition variables to signal between threads

lock
- ensure that any critical section (that a lock umkringir) executes as if it were a single atomic instruction
- a lock is either
	- available
	- acquired
- Can store other info in the data type
	- the thread that holds the lock
	- queue for ordering lock acquisistion
	- (this is hidden from the user of the lock)
- Allow minimal control over scheduling for programmers
- Evaluation of locks
	- does it provide mutual exclusion (and how well?)
	- does each thread contending for lock get fair shot at acquiring once lock is free (fairness) (does starvation occur)
	- what time overhead is added (performance)
		- one thread
		- many threads on same CPU
		- many threads on different CPUs
- Implementations
	- Disabling interrupts
		- A privileged instruction -> only feasible in kernel
		- really simple
		- reaaally dangerous
			- endless loop requiring restart
			- lost interrupts
		- doesn't work with multiple CPUs
	- Flag variable
		- faulty with race condition
		- check var == 0, set var = 1, do stuff, set var = 0
		- if var == 1, spin wait ()
		- doesn't work (race condition) -> spin wait bad (most of the time)
	- test-and-set (atomic exchange) instruction
		- hardware instruction
			- int TestAndSet(int \*old_ptr, int new) {
				  int old = \*old_ptr;
				  \*old_ptr = new;
				  return old
			  } (atomically)
			- used with:
				  while (TestAndSet(&lock->flag, 1) == 1); // spin!
			- unlock sets lock flag back to 0
	- Compare-and-swap / compare and exchange
		- hardware primitive
		- test if value at address specified is equal to expected
			- ? update the memory location pointed to by ptr with new value
			- : do nothing
			- return the orignal value at that memory location
		- more powerful than test-and-set
			- lock-free synchronization
		- but can also just create spin lock if we want
	- load-linked and store-conditional
		- hardware instructions
		- load-linked
			- works like a load instruction 
				- fetches a value from mmory and places in a register
		- store-conditional
			- only succeeds if no intervening store to the address has taken place
				- updates the value stored at the address just load-linked from)
			- success ? 1 : 0
	- fetch and add
		- hardware primitive
		- atomically increments a value while returning the old value at a particular address
			- int fetchAndAdd(int \*ptr) {
				  int old = \*ptr;
				  \*ptr = old + 1;
				  return old
			  }
		- can be used to create a ticket lock

X86 instructions
- fetch and add XADD
- exchange contents of two memory words SWAP XCHG
- Compare and exchange CMPXCHG
- CMPXCHG8 -> 64 bit
- CMPCSH16B -> 182 bit

Atomic store operations
- a variable that says whether a lock is active or not


Spinlock limitations
- simple and efficient 
- Don't work well if 
	- contention is high
	- if CS is large
	- if threads are on different cores (memory needs to be kept coherent between cores, which is expensive)
	- if static priorities
		- needs priority inversion
- analysis of yield as a solution
	- the cost of a context switch can be substantial
	- bad performance in case of many threads
		- while (lock unavailable) yield -> cycles through threads with context switches if many threads

Blocking locks
- sleep while waiting

Properties of atomic store operations
- Mutual exclusion
- progress
- no upper bound on waiting
- (if spinning) bad performance

Spin lock
- The simplest type of lock to build
- spins, using CPU cycle, until the lock is available
- Requires a preemptive scheduler (non-cooperative)
- Works (if implemented correctly)
- Unfair (a thread could starve, lock is acquired in random order)
- performance
	- single core -> bad, wasting CPu cycle
	- multi core  -> OK, sometimes good if critical section is very short
- priority inversion
	- Assume two threads in a system
		- T2 has high scheduling priority
		- T1 has low scheduling priority
		- if both are runnable, T1 only runs when T2 is not able to do so
		- I.e. high priority thread wait for low priority thread 
			- takes a long time, or never happens
		- solution
			- priority inheritance
				- high prio thread can boost prio of lower prio thread that holds the lock


When to spin and when to block
- no real way to calculate real time
- just use hybrid lock if you don't know
- two-phase lock
	- try to get in CS with spinlock
		- leave CS if no thread is waiting, else wakeup a bloccked thread
	- if cs is busy use a syscall to put thread to sleep
		- only woken up when thread becomes fre

non-blocking synchronization
- design algoritm to avoid critical sections
- requires atomic instructions that atomically set state babsed on condition
- can implement common data structures lockless
	- stacks
	- queues
	- hash tables
- does not guarantee better performance 
	- not really faster
	- more scalable
- benefits
	- thread-killing immunity
		- any thread forcefully killed in the system won't delay other threads
		- (thread with locked killed)
	- signal immunity
		- signal handlers (interrupt handlers9 must not call functions that use locks 
		- signal handler may run while that function is holding a lock
			- deadlock!
		- interrupt handlers shouldn't allocate memory
	- priority inversion immunity
		- no blocking if lower level thread holds lock


Ticket lock
- use ticket and turn variable in combinatiuon to build a lock
- implementation
	- when a thrad wishes to acquire a lock, it does an atomic fetch-and-add on the ticket value
	- that value is now considered this thread's turn
	- lock->turn is then used to determine which thrad's turn it is
	- when myturn == turn for a given thread, it is that thread's turn to enter the critical section
	- unlock is accomplished by incrementing the turn such that the next waiting thread can now enter the critical section
- benefits
	- ensures progress for all threads
	- once a thread is assigned its ticket value, it will be scheduled at some point in the future

Contention (locks)
- if there are many threads contending for a lock there is contention
- if there is only one thread then there is no contention
- low to high

how to stop spinning - a guide for locks
- Needs OS support for a yield operation
	- Let thread give up their CPU cycle
	- while (condition) yield; // !!
	- still incurs the cost of context switching (but not of waiting n many CPU cycles)
	- There is still starvation
- Use queues : sleep instead of spinning
	- lock == available
		- ? set lock = unavailable ; do stuff ; wake up next thread
		- : put self on queue ; put self to sleep
	- park() and unpark(threadId)
		- sleep, and awaken
	- some spinning still while waiting for access to the queue lock
	- flag is not set to 0 between passing the lock between threads
	- A dangerous race condition wakeup/waiting race
		- puts self on queue
		- then sleep
		- if interrupted there between
		- and lock is passed to the thread, then the lock will not actually wakeup, but get activated then go directly to sleep, holding the lock forever.
		- reqiores a setpark() to fix
			- I'm about to park! -> aaand parking (if passed between then awoken straight away)

Linux futex
- futex_wait(address, expected)
	- puts calling thead to sleep, assuming the value at address is equal to expected. If it is not equal, the call returns immediately
- futex_wake(address)
	- wakes one thread that is waiting on the queue

two-phase locks
- Lock spins for a while, hoping that it can acquire the lock
- if it has waited long enough it goes to sleep


Condition variables
- An explicit queue that threads can put themselves on when some state of execution (condition) is not as desired (by waiting on the condition)
	- Some other treahd, when it changes said state, can then wake one (or more) of those waiting threads and thus allow them to continue (by signaling on the condition)
- When a thread wishes to check whether a condition is true before continuing its execution
- how
	- wait, when threads wishes to put itself a sleep
		- takes mutex as a parameter, assumes that this mutex is locked when wait is called
		- wait releases the lock and puts the calling thread to sleep (atomically)
		- when awoken, must reacquire the lock before returning to caller
	- signal(), when a thread has changed something in the program and thus wants to wake a sleeping thread waiting on this condition
- how to use
	- keep state in addition to CVs
	- always do wait / signal with lock held
	- whenever thread wakes from waiting recheck state


The producer/consumer -> bounded-buffer problem
- One or more producer threads and one ore more consumer threads
	- producers
		- gernate data items and place them in a buffer
	- Consumers
		- grab said items from the buffer and consume them in some way
- The buffer is a shread resource
- Mesa semantic
	- after being woken up, there is no guarantee that the condition still holds
- Hoare semantic
	- much harder to implement, but the condition is guaranteed to hold
- Solution
	- use while loops on the condition waits
	- use two condition variables
		- so that a consumers can only wake producers and producers can only wake consumers.
- Solution with semaphore
	- sem_init(&empty,0, MAX); -> as many resources available as buffers free
	- sem_init(&full, 0, 0); -> 0 tasks for consumers available
	- needs some kind of locking in put and get as well


Spurious wakeups
- due to the way some thread libraries are implemented wake can awaken more than one  thread

covering condition
- pthread_cond_broadcast() -> wake up all waiting threads (CV)
- many threads are woken up at once, so the right thing is bound to happend, but with a performance impact


Concurrency objectives
- mutual exclusion
- ordering
	- condition variables and semaphores

Generalized semaphore (semaphore)
- can be used as either a lock or a condition variable
- A semaphore is an object with an integer value that we can manipulate with two routines
	- sem_wait(sem_t \*s)
		- decrement value of semaphore by 1
		- val >= 0
			- ? return right away
			- : causes caller to suspend execution to wait for subsequent post
				- multipler threads may call into sem_wait() and be queued waiting to be woken
	- sem_post(sem_t \*s)
		- Does not wait for some condition to hold. Increments the value of the semaphore and then, if there is a thread waiting to be woken, wakes one of them up
- The value of the semaphore, when negative, is equal to the number of waiting threads.
- wait == sleep
- Semaphores must be initialized to some value
	- the initial value of the semaphore determines its behavior
		- \#include \<semaphore.h>
		- sem_t s;
		- sem_init(&s, 0, 1);
			- initialize to 1, 
			- 0 indicates that the semaphore is shared between threads in the same process
				- can also be used across different processes

CV vs semaphore
- Condition variables have no state (other than waiting queue)
	- programmer must track additional state
- semaphores have state : track an integer value
	- state cannot be directly accessed by user program, but state determines behavior of sempaphore operations
	- each semaphore has associated wake-up queue
		- weak semaphores -> wake up randome waitin thread on post
		- strong semaphores -> wake up thread strictly in the order in which they started waiting

Equivalence claim for semaphores
- locks can be built from semaphores
- condition variables can be built from semaphores
	- possible but really hard
- semaphores can be built from locks + condition variables

Semaphore as a lock -> binary semaphore
- a semaphore that is used as a lock
- surround the critical section of interest with sem_wait() -> sempost() pair
	- The initial value of the semaphore is critical
	- For a reguler lock, this value shoould be 1

Semaphores for ordering
- order events in a concurrent program
	- one thread waits for something to happen
	- another thread makes that something happen, then signals that it has happened
- Initial value of semaphore is 0 for this case
	- parent waits for child
	- parent calls sem_wait() -> -1
	- child calls sem_post() directly -> 0
	- parent can run


Rule for semaphore initialization
- consider the number of resources you are willing to vie away immediately after initialization
	- 1 -> lock the lock immediately
	- 0 -> nothing to give away quite yet


reader-writer locks
- different types of accesses require different types of locking
- as long as there is no write, we can read safely
- use semaphores
	- lock for modifying number of readers
		- first reader acquires the write lock
		- last reader lets it go
	- write lock for writing
		- writer just waits for all readers to finish
- Often add too much overhead to actually be useful

Simple and dumb is often faster than Complex and elegant


Dining Philosopher's problem
- 5 philosophers , 5 forks
- each pilosopher needs to hold two forks to eat
- need to 
	- avoid deadlock
	- avoid starvation
- everybody starts by grabbing right fork, except one philosopher
	- avoids deadlock entirely

Semaphores for thread throttling -> admission control for threads
- avoid allowing too many threads doing something at the same time
	- i.e. to limit the number of threads concurrently executing the piece of code in question
- use binary lock (with semaphores) and set the initial value to the maximum amount of threads you want to let in.


Zemaphores
- semaphores but don't maintain that when the value is negative it reflects the number of threads waiting.

Building condition variables out of semaphores is tricky, but possible



concurrency issues
- non-deadlock bugs
	- atomicity violation
		- critical section is not actually protected by anything
		- the desired serializagility among multiple memory accesses is violated
		- a code region is intended to be atomic, but the atomicity is not enforced during execution
		- add a fucking lock
	- order violation
		- The desired order between two (groups of ) memory accesses if flipped, the order is not enforced durin execution
		- condition variables help fix this
		- or semaphores
- Deadlock bugs
	- Four conditions required for deadlocks to occur
		- Mutual exclusion
			- thread claims exclusive control of resources that they may required
		- Hold-and-wait
			- threads hold resources allocated to them, while waiting for additional resources
		- no preemption
			- resources cannot be forcibly removed from threads that are holding them
		- Circular wait
			- there exists a circular chain of threads such that each thread holds one or more resources that are being requested by the ext thread in the chain
	- Prevention techniques
		- Write your code such that a circular wait never occurs.
			- provide a total ordering on lock acquisition
				- e.g. 2 locks, always acquire lock 1 before lock 2
			- total ordering -> always accquire locks in some order
			- partial ordering
				- a comes before b, which comes before c -> for some groups of locks
			- Effective but requires deep understanding and control of the code
		- Hold and wait can be avoided by acquiring all locks at once, atomically
			- i.e. use a lock lock, and only lock the locks if you have said lock lock
				- ensures that all lockings reach a finish line of some kind
			- decreases concurrency, difficult in cases of encapsulation
		- preemption
			- trylock
				- fail if lock is held -> unlock then try again
					- can result in a livelock
					- i.e. both programs doing the same thing, but always getting into trouble because the other has locked some part
					- basically endless while loop on two ends
		- Avoid mutual exclusion
			- difficult, but possible if the right hardware instructions are available
	- Deadlock avoidance
		- scheduling
			- smart scheduling that avoids running contending threads at the same time
			- one must have full knoledge of the entire set of tasks that must be run, and the locks that they need
		- state
			- on every resource request
				- decide if system stays in safe satate
					- needs a-priori information
	- Detect and recover
		- allow deadlocks to occasionally occur, then take some action once suc a deadlock has been detected
			- if deadlocks are rare, this is OK
		- Database
			- deadlock detector runs periodically, building a resource graph and checdking it for cycles
			- if cycle, the system restarts. may need to call human to ease the process
		- Maintain wait for graph
			- periodically invoke an algorithm that seraches for a cycle in the graph
				- do something about it
					- select a victim
						- abort all deadlocked
						- abort one at a time until fixed
					- rollback
						- perform periodic snapshots
						- abort process to preempt resources
						- restart process from saved state
					- starvation
						- same process may always be picked as victim
						- include number of rollbacks in cost factor
Deadlock prevention solutions
- mutual exclusion
	- buy more resources, split into pieces, virtualize to infinite number of instances
- hold and wait
	- get all resources en-bloque
		- release all locks before acquiring all locks necessary for the next phase
		- problem resource utilization and starvation
- no preemption
	- virtualize to make preemptable (applicable for resources that can be saved and restored)
		- virtual vs physical memory
- circular wait
	- ordering of resources

Scheduling proportional share
- fair-share scheduler
- nstead of optimizing for turnaround or resonse time, guarantee that each job obtains a percentage of CPU time
- types
	- Lottery scheduling
	- stride scheduling


Fair-share scheduling issues
- do not mesh well with IO
- what should the priority be?

Lottery scheduling
- use tickets
	- represent the share of a resource that a process (or someone) should receive
	- the percent of tickets that a process has, represents its share of the system resource in question.
- holding a lottery
	- lottery scheduling achieves this probabilistically (not deterministically) b holding a lottery every so often (e.g. every time slice)
	- scheduler must know how many total tickets there are, then pick a winning ticket
	- scheduler then loads the state of the winning process and runs it.
- ticket currency
	- allows users to give whatever process some currency to boost their priority
- ticket transfer
	- a process can temporariliy hand off its tickets to another process
- ticket inflation
	- a process can temporarily raise or lower the number of tickets it owns
		- if needs more attention or less attention
	- (in a scenario where the process trusts other processes)
- Implementation
	- random number generator
	- data structure to track processes of the system
	- track total tickets
- handing out tickets
	- Allow user to do it?


Stride scheduling
- a deterministic and fair scheduler
- what
	- each process in the system has a stride (the inverse in proportion to the number of tickets it has)
	- every time a process runs, we increment a counter for it (the pass value) by its stride to track global process
	- use stride and pass to determine which process should run next
		- at any given time, pick the process to run that has the lowest pass value so far.
		- when run, increment by the stride
	- Stride scheduling gets the proportions right at the end of every scheduling cycle
	- A global state
		- a new process entering in the middle of a scheduling cycle messes everything up.

Global vs. local page replacement
- global -> can take any frame
- local
	- frames assigned to application
	- frame can only pick from those frames
	- benefits
		- faster algo for picking
		- guaranteed frame availability
	- cons
		- no adapting to changing memory demands
		- voodoo constant

The linux completely fair scheduler
- Goal
	- fairly divide a CPU evenly among all competing porcesses
	- uses counting-based technique know as virtual runtime (vruntime
		- as each process runs, it accumulates vruntime
		- when a scheduling decision occurs, CFFS will pick the processwith the lowest vruntime to run next
- The faster it switches the more fair it is, but the more overhead for context switching as well
- two parameters
	- sched_latency
		- this value / n = time slice afforded to a process
	- min_granularity
		- the minimum amount of time a process can run
	- Scheduler wakes up to inspect everything every once in a while
- allows weighting (niceness)
- needs fast lookup for processes
	- use red black tree
		- for running / runnable processes
- on wake up
	- set vruntime to the minimum found in the tree
	- Jobs that sleep for short amounts of time, frequently don't get fair share


The advantages of random approaches
- avoids corner-case behaviors that traditional algorithms may have trouble handling
- lightweight, requiring little state to track alternatives
- can be very fast, as a result of how simple it is
	- but, the faster the need, the more pseudo-randomness occurs



RAID - redundant arrays of inexpensive disks
- A technique to use multiple disks in concert to build a faster, bigger and more reliable disk system
	- externally, looks like one large disk
		- Works transparently
		- don't have to change anything in software to go from regular disk to raid
	- internally - complex, consisting of multiple dissks, memory (volatile and non-volatile, and one or more processors to manage the system)
- Benefits
	- better performance
		- using multiple disks in parallel
	- larger capacity
	- improved reliability
		- can tolerate loss of a disk, and keep operating as if nothing were wrong
	- Deployable (transparent interface)
- Fault models
	- RAIDs are designed to detect and recover from certain kinds of disk faults
	- knowing which faults to expect is critical in arriving upon a working design
	- types
		- fail-stop
			- a disk can be in one of two states : working or failed
				- working -> all blocks can be read / writen
				- failed  -> assume data is permanently lost
- RAID evaluation
	- capacity
		- given a set of N disks with B blocks, how much useful capacity is available to clients of the RAID?
			- w/o redundancy N * B
			- mirroring (N \* B) / 2
	- Reliability
		- How many disk faults can the given design tolerate
	- Performance

RAID chunk sizes
- affects performance of the array
- small chunk implioes
	- many files will get striped across many disks, thus increaseing parallelism of reads and writs to a single file
	- positioning time to access blocks across multiple disks increases
		- positioning time is determined by the maximum over all drives
- big chunk size implies
	- reduced intrar-file parallelism
	- reliable on multiple concurrent requests to achieve high throughput
	- reduced positioning time
- Choosing the correct size
	- depends on the wworkload presented to the disk system
- How many contiguous blocks are placed on each disk


RAID level 0 : striping
- no redundancy
- excellent upper-bond on performance and capacity
- Stripe blocks across the disk of the system
- 1 to disk 1, 2 to disk 2, x to disk x % nDisks
	- or similar
- offset is x / nDisks
- reliability
	- if a disk dies, everything is fucked
- Performance
	- single-request latency -> same as regular disk
	- steady-state sequential throughput
		- expect to get the full bandwidth of the system, throughput equals N (number of disks) multiplied by S (the sequential bandwidth of a single disk)
			- N * S
	- steady-state random throughput
		- use all disks, and get N * R MB /s


RAID level 1 (Mirroring)
- opposite of level 0
- make more than one copy of each block in the system
	- each copy is placed in a separate disk
- can tolerate disk failures
- on read
	- read either!
- on write
	- update both  :( (but can be done in parallel)
- analysis
	- Capacity 
		- is halved (over the actual capacity we have)
	- reliability
		- quite good, tolerates failure of any disk
		- or 1 failure for certain, and up to N/2 failures!
	- performance
		- latency of read = as one disk
		- write is done in parallel but still twice, so suffers the worse latency of the two
		- steady-state throughput 
			- sequential
				- N/2 * S throughput (half the peak bandwidth.) for read and write
			- Random
				- best case for RAID 1
				- N * R MB/s
				- distributes reads across all disks and thus obtains the full possible bandwidth
				- random write N/S


RAID 1 + 0 and RAID 0 + 1
- RAID 1 + 0 (stripe of mirrors)
- Skoða


parity-based-redundancy
- attempt to use less capacity and thus overcome the huge space penalty paid by mirrored systems
- come at a performance coset
- parity is the XOR
- the number of 1s in any row, including the parity bit, must be an even (not odd) number (invariant that raid must maintain in order for parity to be correct)




RAID level 4 (parity-based-redundancy)
- For each stripe of data, add a single parity block taht stores the redundant information for that stripe of blocks 
- analysis
	- capacity = (N - 1) * B
	- reliability
		- tolerate 1 disk failure and no more
	- performance
		- steady-state throughput
			- seq read
				- can use all disks except parity -> (N - 1) * S MB/s
			- seq write
				- can do full-stripe write -> most efficient
				- (N - 1) S Mb/s
			- rand read
				- R(N-1) MB/s
			- rand write
				- additive parity
					- read all other data blocks in stripe (in parallel) and xor those with the new block a lot of extra reads
				- subtractive parity
					- read block -xor to parity along with the new data, write parity, write block
			- latency is about the same as regular disk (but twice as slow for write))

Small-write problem for parity-based RAIDs
- parity disk is a bottleneck
- 2 writes on different disks
	- but both require writes to different parity blocks
	- and both require reads from all other disks (when additive parity)
	- i.e. less parallelization


RAID level 5 (parity-based-redundancy)
- rotating parity
- addresses the small-write problem
- works almost identically to raid-4 but rotates the parity blocks across dirves
- analysis
	- basically same as raid 4 except
		- random read perfromance is a little better (utilize all disks)
		- random write perofmrance improves noticably
			- allows for parallelism across requests
			- bandwidth for small writes
				- = N / 4 * R MB/s (4 memory accesses)


RAID performance
- two metrics
	- single-rerquest latency
		- single IO request
		- reveals how much parallelism can exist during a single logical IO operation
	- Steady-state throughput
		- total bandwidth of many concurrent requests

Throughput
- two types of workloads
	- sequential
		- requests to the array come in large contiguous chunks
	- random
		- assume that each request is rather small and that each request is to a different random location on disk
		- e.g. transactional work on DBMS

when to pick
- reliability -> raid 1 : mirror
- performance -> raid 0 : stripe
- capacity and reliability : raid 5
- large seq IO : raid 5






------

I/O devices

busses
- general I/O bus -> high performance IO devices
- peripheral bus -> slow devices
	- SCSI
	- SATA
	- USB
	- disk, mice, keyboards

DMI - direct media interface
- CPU connects to an O chip via DMI
- other devices connect to this chip via a number of different interconnects

PCIe - peripheral component interconnect express
- connects high performance devices to the CPU through the DMI
- PCIe graphics can connect graphics straight to the CPU
- Network and high performance storage devices NVMe connect here as well


Canonical device
- hardware interface
	- allows the system software to control its operation
	- abstract
		- the OS controls device behavior by reading and writing to registers
		- three registers
			- status register
				- can be read to see current status of device
			- Command register
				- tell the device to perform certain tasks
			- data register
				- pass data to the device or get data from the device
		- The canonical protocol
			- 4 steps
				- wait for access to device (until not busy with other stuff)
				- write data to DATA register
				- write data to COMMAND register -> starts device and executes command
				- wait until device is done with your request
					- polling in a loop -> waste CPU time by just waiting
					- ask for interrupt -> wait for interrupt
						- OS issues a request, puts the calling process to sleep, and context switches to another task
						- when the device is finished , raise hardware interrupt, causing cpu to jump into the os at a predetermined interrupt service routine ISR -> interrupt handler
						- interrupt handler finishes the request
							- read data or error from device
							- details
								- can send one segment at a time, or batch, and send everything at once
						- then wakes the processs waiting for the IO, which can then proceed as desired
						- Allows for overlap
						- beware 
							- significant overhead -> context-switching and interrupt handling is slow
							- a flood of interrupts may overwhelm the system and lead to a livelock
					- coalescing
						- after device is finished, wait a bit before delivering interrupt
						- then send multiple interrupts at once
					- what/when
						- polling -> when device is very fast
						- interrupt -> when device is slow
						- hybrid -> when unknown
- internal structure
	- implementation specific, responsible for implementing the abstraction the device presents to the system
	- may include hardware chips, simple CPUs, general purpose memory etc.


Efficient data movement
- moving data can be a heavy load on the CPU (especially with PIO)
	- also a very simple task that can take a lot of time
	- Copy one word at a time
- use DMA


DMA - direct memory access
- an engine that's essentially a very specific device within a system that can orchestrate transfers between devices and main memory without much CPU intervention
- CPU tells DMA
	- where the data lives in memory
	- how much data to copy
	- which device to send to
	- (after that the CPU is free to do something else)
	- DMA delivers an interrupt once the transfer is complete

Programmed I/O PIO
- when the main CPU is involved with the data movement


Firmware
- software within a hardware device

Device communication
- two primary methods
	- 1. explicit IO instructions (old method)
		- specifya way for the OS to send data to specific device registers and thus allow the construction of the protocols described above
		- example
			- in and out instructions
		- privileged instructions
			- protection
			- what if every program could write directly to disk?
	- 2. Memory mapped IO
		- hardware makes device registers available as if they were memory locations
		- hardware issues load (read) or store (write) to the address
			- routes the load / store to device instead of main memory
		- Nice becuase no new instructions are needed to support it
	- (both equal, but point above ^)


device driver
- solves the problem of device neutrality, i.e. genralizing access to devices
	- problem -> too general? can't really add more features becuase other stuff doesn't do it as well.
- a piece of software in the OS that knows in detail how a specific device works
- any specifics of device interaction are encapsulated within
- represents a huge percentage of the kernel code
- primary contributors to kernel crashes


Description of how a read / write works
- the POSIX API talks to the generic block interface (block read / write) in the generic block layere, which talks to the specific block interface (device driver)
- a raw interface also exists
	- which enables special applications -> such as low-level sotrage management apoplications ,to skip the file abastractions and directly read / write blocks

hard disk drive
- interface
	- drive consists of a large number of sectors
		- each sector = 512 byte block
		- each can be read or written
		- marked 0 to n -1 on a disk with n sectors
	- disk viewed as an array of sectors -> address space of the drive
	- only a write of 512 bytes is atomic
		- even though many FSs allow read or write to 4KB at a time (multi-sector operations)
	- the unwritten contract of disk drives
		- assumptions most clients of disk drives make, but are not speicified directly in the interface
		- accessing two blocks near one-another within the drive's address space will be faster than accessing two blocks that are far apart
		- accessing blocks in contiguous chunks is the fastest access mode
- A modern disk
	- A platter
		- circular, hard surface on which data is stored persistently by inducing magnetic changes to it.
		- a disk may have 1 or more platters
		- each platter has 2 sides (side = surface)
		- coated in magnetic layer that enables the drive to store bits
	- surface
		- a side of a platter
		- contains data, stored in tracks
		- contains thousands of tracks, tightly packed together
	- Spindle
		- Platters are bound together around the spindle
		- the spindle connects to a motor that spins the platters around at a fixed rate
			- RPM
			- 7200 - 15000 RPM typically
	- Data
		- is encoded on each surface in concenctric circles of sectors
		- each concentric circle is called a track
	- track 
		- stores the actual data
	- disk head
		- reads and writes data -> senses or induces a change in the magnetic patterns on the disk
		- one head per surface 
		- attached to a single disk arm
	- disk arm
		- moves across the surface to position the head over the desired track
- disk issues
	- single track latency -> rotational delay
		- the time it takes to wait for the desired sector to move below the disk head
	- seek time -> with multiple tracks
		- the time it takes to move to the right track
		- steps
			- acceleration
			- coasting
			- deceleration (settling)
				- often the most significant part as zeroing in on the right track can be difficult, given the of tracks
				- 0.5 - 2 ms
- IO time with disk
	- seek
		- average seek time is about 1/3 of the full seek time
	- track
	- transfer -> time to write / read data from / to the surface
	- formula
		- TI/O = Tseek + Trotation + Ttransfer
- other 
	- track skew -> positioning continuing numbers in such a way that once the seek is finished the tracking is finished right away when accessing contiguous blocks
	- outer tracks tend to have more sectors than inner tracks
		- multi-zoned disk drives
		- the disk is organized into multiple zones, where a zone is a consecutive set of tracks on a sruface
		- each zone has the same number of sectors per track
	- cache -> track buffer
		- 8 - 16 MB which the drive can use to hold data read from or written to the disk
		- a drive might f.x. read all sectors from a track and cache in memory (sinse seeking and tracking is done, this is super fast and easy)
	- write back vs. write through
		- write-through
			- any update to a given memory location applies to cache and main memory
			- main memory is always up to date
		- write-back
			- only cache updated on modification (dirty bit set)
			- main memory updated once evicted
	- write-allocate ->  load to cache then write
	- write-to-memory -> don't load in cache


random vs. sequential workloads
- infer different times for IO
- random -> accessing memory in random order
- sequential -> accessing contiguous blocks of data, in order

rate of IO
- transfer size / TIO

Disk scheduling
- historically teh OS decides the order of IO issued to the disk
- with disc scheduling we can make a good guess at how long a job will take
- the disk scheduler will try to follow SJF
- SSTF
	- an early disk scheduling approach (shortest seke time first)
	- pick requests on the nearest track to complete first
	- BUT the OS isn't aware of disk geometry, therefore use NBF -> nearest block first
	- starvation!! is an issue
- Elevator SCAN or C-SCAN
	- an algorithm that moves back and forth across the disk servicing requests in order across the tracks
	- a single pass accross the disk, form outer to inner tracks is called a sweep
	- C-SCAN
		- scan only from outer to inner
		- more fair to the middle tracks
- SPTF -> shortest positioning time first / SATF -> shortest access time first
	- usually done inside the disk
- Scheduling in modern systems
	- the OS picks a couple of requests that it thinks is best and issues to disk
	- the disk then uses its internal knowledge to service said requests in the best possible (SPTF) order
- IO merging
	- a task performed by disk schedulers
	- merging read requests into simpler reads
		- say,  33, 8 , 34 -> 33-34, 8
- when to issue IO to disk
	- wait a bit - conserve work
	- so that you can pick a better ordering of requests


The virtualization of storgae
- file
	- a linear array of bytes that can be read or written to
	- has a low-level name -> number
		- also called inode number (i-number)
- directory
	- like a file
	- has low-level name
	- specific contents (unlike a regular file)
		- a list of pairs
			- user-readable name
			- low-level name

The directory hierarchy / directory tree
- directories within directories storing all files and directories
- root directory
	- / on unix
- directories and files can have the same name, as long as they are in different locations in the file-system tree
- file extensions are usually jsut a convention

file system contains
- files,
- devices
- pipes
- processes


Filesystem
- OS does not know much about the structure of the file (is picture, text, c code?)
- responsibility of the file system is simply to store such data persistently on disk and make sure that when you request the data again, you get what you put there in the first place


The file system interface
- create
	- accomplished with the open system call
	- open parameters
		- O_CREAT
			- creates file if it does not exist
		- O_WRONLY
			- ensures that the file can only be written to
		- O_TRUNC
			- if file exists, truncate to 0 bytes (remove all its contents)
	- open returns a file descriptor
- access
- delete
- unlink()
	- used for removing files

each file already has 3 open files
- standard input
- standard output
- standard error


file descriptors
- an integer, private per process
- used in UNIX systems to access files
- a capability
	- an opaque handle that gives you the power to perform certain operations
- a pointer to an object of type file
- managed by the OS on a per-process basis
	- some kind of simple structure is kept in the proc structure on UNIX systems in an array of open files for the process
	- pointers to a struct file that contains info about the file
	- array of file descriptors -> each referring to an entry in the system-wide open file table
		- each entry in the table tracks which underlying file descriptor refers to, the current offset, and other relveant details, such as whether the file is readable or writable


strace - dtruss on mac
- trace system calls a program makes, see arguments and return codes
- -f follows fork'd children too
- -t reports time of day
- -e trace=open,close,read,write only traces those calls

lseek
- used for random offset within the document
- whence 
	- SEEK_...
		- SET -> from start
		- CUR -> current
		- END -> size of file + offset
- just changes a variable - has no direct effect on the device itself


proc !!


the file struct 
- referenced by proc
- includes
	- ref --> reference count
	- readable
	- writable
	- inode \*ip
	- uint off; --> current offset from within the file

The open file table
- an array of file structs -> representing all currently opened files in the system
- despite that, opening the same file twice, creates two structs that are updated independently
	- exceptions to this are when using fork and dup
		- ref++
		- only deleted from the open file table once all references are gone


fsync()
- write straight to file (don't wait!)
- sometimes you may need to fsync write both the file and the directory!
	- so that the file is actually accessible :)
- why
	- writes are usually left unhandled for a little bit, then done later -> the book says every 5 or 30 seconds!


directory operations
- rename()
	- atomic -> if crash, then the name will either be the old one or new one (no inbetween states)
	- can be used for atomic file update


memory mapping
- an alternative way to access persistent data in files
- mmap() system call
	- creates a correspondence between byte offsets in a file and virtual addresses in the calling process
		- file -> backing file
		- virtual addresses -> in-memory image
	- can access the backing file using CPU instructions loads and stores to the in-memory image
- combines the persistence of files with the access semantics of memory
	- persistent memory
- eliminates translation between different data formats for memory and storage


stat or fstat -> see metadata about files
- data stored in an inode


unlink() system call
- takes the file to be removed and returns zero upon success

link() system call
- takes two arguments -> an old pathname and a new one
- creates a way to refer to the same file
- the command line program ln does this
- creates a new name in the directory and links it to the same inode number of the original file
	- you can see the inode number with ls -i filename

Hardlinks
- use the link() system call
- link inode to a new name
- files are indistiguishable to the file system
- can't create one to a directory -> otherwise you might create a cycle
- can't hardlink to files in other disk partitions
	- inodes are unique only within a particular file system
- Each directory entry is a hardlink
- not processes by VFS -> individual file system

Symbolic links -> soft link
- ln -s
- creates a file in its own right -> different from hard link
- l -> filetype in ls -a, also see what file is linked to
- stores only the pathname of the linked-to file
- can become a dangling reference if original file is deleted
- content interpreted by VFS layer


creating a file
- make an inode
	- a structure that will track virtually all relveant informaition about the file
- link the inode to a human-readable name to that file


directories
- The file system is responsible for the integrity of directory data
	- you cannot write to a directory directly
	- indirectly
		- create files, directories or other object types within it.
- regular files whose type is directory, and whose structure is well known to the FS
	- a list of records (of fixed or variable length) consisting of at least
		- filename
		- inode number
- operations
	- create
		- mkdir creates the directory
		- created with two files . and ..
		- links to self, and parent
	- read
		- ls reads directories
		- systemcalls
			- opendir()
			- readdir()
			- closedir()
		- ls -l 
			- reads each files inode with the stat command
	- delete
		- rmdir -> but the directory must be empty


Simple file system implementation - vsfs (VERY simple file system)


impelementing inodes
- inode region -> storing inodes
- data region -> storing data blocks for inodes to point to
- inode bitmap -> bitmap of free inodes
- data bitmap -> bitmap of free data
- Superblock
	- contains information about this particular file system
		- how many inodes and data blocks are in the file system
		- where the inode table begins
		- magic number to identify the file system type
		- etc.
- required data
	- file size
		- to deal with files that are not a multiple of blocksize in length
	- file type
		- used to traverse directory hierarchy
	- number of hardlinks
		- know when to delete
		- if 0, the inode and data blocks are marked deleted / for deletion
	- Access rights
		- contained but only informational
	- timestamps
		- optional but useful for some things
	- ordered list of (data) block numbers


Types of file access
- sequential access
- direct access


getdents
- system call used to list directory entries (of a specific directoy)



inode
- a persistent data structure kept by the file system
- all inodes reside on disk
	- a copy of active ones are usually cached in memory to speed up access
- multi-level index approahc
	- direct pointer -> a data block
	- indirect pointer
		- points to block containing more pointers, each pointing to user data
		- double and triple also exist.
	- why?
		- most files are small
- direct pointer alternative
	- extent
		- a disk pointer plus a length (in blocks)
		- uses less metadata per file
- zero is a reserved inode number indicating deletion

directory
- for each file or directory in a directory, there is a string and a number in the data blocks of the directory, though there may also be length
- storing directories
	- stored like any type of file, but the type field is marked as directory
	- dat blocks pointed to by the inode -> storing the filename, inode mapping
	- sometimes heavy data structures such as B trees used here.

linked-list approaches to persistently store data
- you can do a linked list
- end of file is next pointer
- or store table with these next pointers -> next pointer doesn't need to be in file actually
- FAT -> file allocation table

free space management in file systems
- find free blocks
- sometimes try and find sequences of free blocks so that a new file can lay contiguously in memory

mounted 
- file system is activated (superblock is in memory)

root
- in most unix file systems -> inode number = 2

final steps of reading from pathname
- read inode into memory
- final permission check
- allocate a file descriptor in the per-process open-file table, return to user
- on read
	- read first block of file
	- update inode with new last accessed time
	- in-memory  file table updated for the file descriptor (offset)


writing
- each write logically generates five IOs
	- one to read data from bitmap -> then updated
	- one to write the bitmap
	- two more read and then write the inode, updated with the new block's location
	- one write the actual block itself
- creating a new file harder
	- then also need to look at and update inode bitmap
	- and directory
	- creating a file SKOÐA 535


caching 
- DRAM -> system memory to cache imporant blocks
- fixed size cache
	- old 
		- 10% of memory
		- allocated at boot
	- static partitioning of memory can be wasteful
- dynamic partitioning
	- new
	- integrate virtual memory pages and file system pages into a unified page cache
	- integrate virtual memory pages and file system pages into a unified page cache
	- memory can be allocated more flexibly across virtual memory and file system, depending on which needs more memory at a given time

write buffering
- delaying writes (to disk, just storing it in cache or something)
- benefits
	- batch some pupdates into a smaller set of I/Os
	- greater capacity to schedule I/Os efficiently
	- no writing temporary files to memory
- most modern systems buffer writes in memory for 5 - 30 seconds
	- can result in lost data
	- durability / performance trade-off
		- can't tolerate loss of data
			- write straight to disk -> slow but safe
		- can tolerate loss of little data
			- buffer writes in memory
			- writes appear to complete quickly -> improving perceived performance, but on crash lose that shit


Static partitioning
- divides the resource into fixed proportions once
- benefits
	- ensures each user receives some share of the resource
	- more predictable performance
	- easier to implement

Dynamic partitioning
- flexible
- differing amounts of the resource over time
- benefits
	- better utilization
	- complex to implement
	- can lead to worse performance for users whose idle resources get consued by others



Permission bits (UNIX)
- first slash is type of file
	- d - directory
	- l - symbolic link
	- - - regular file
	- c - character device 
	- b - block device
- groupings
	- owner
	- group
	- other
- letter meanings
	- r
	- w
	- x -> can be run / not
- letter meanings on directory
	- r
	- w
	- x -> execute -> operations the directory, e.g. delete / create a file.
		- delete file
		- create file -> if writable bit is set as well
		- cd into directory
- owner can change these permissions
- and root ->
	- can access all files regardless of privileges



Access control lists -> ACL
- More sophisticated (graunular) controls for permissions
- more general and powerful way to represent who can access a given resource


How to assemble a full directory tree from many underlying file systems
- make files systems, then mount them
- mkfs
	- make file system
	- give it a device (disk partition) and a file system type and it writes an empty file system, starting with a root directoyr, onto that disk partition.
- Once a file system is created, it needs to be made accessible within the uniform file-system tree
- mount
	- makes underlying system call mount()
	- take an existing directory as a target mount point and paste a new file system onto the directory tree at that point
	- the mount point basically becomes the root directory


file
- array of bytes which can be created, read, written, and deleted.
- has a low-level name (a number) that refers to it uniquely -> i-number

directory
- a collection of tuples
	- "human-readable name -> low-level name" mapping
- each entry refers to another directory or to a file
- has low-level name: i-number
- always two special entries
	- . -> self
	- .. -> parent

directory tree / hierarchy
- organizes all files and directories into a large tree, starting at the root

file-descriptorrs
- private, per-process entity
- refers to an entry in the open file table
	- the entry tracks which file this access refers to, current offset in file (next to read / write) + other metadata
	- syscalls read and write update the current offset





Managing memory
- ideal memory properties
	- large
	- fast 
	- nonvolatile
	- cheap


CPU cache location
- buffer memory 
	- for exploiting temporal and spatial locality
	- low latency, high bandwidth
	- recution of main memory accesses
	- reduction of memory bus traffict (important for multiprocessor systems)
	- buffer for asyn prefetch operations


Types of cache misses
- compulsory miss / cold start / first reference
	- data block was not cached before
- capacity miss
	- not all required data fits into the cache
	- accessed data was previously evicted to make room for different data
- conflict miss
	- collision, interference
	- depending on the cache organization, data itmes interfere with each other
	- fully asociative caches are not prone to conflict misses
	- associative 
		- e.g. demands on the ordering of data.

the harvard architecture 
- separate buffer memory for data and instructions

write and replacement policies
- cache hit
	- write through
		- main memory is always up-to-date
		- writes directly to main memory
		- immediate upon change in cache
		- writes may be slow
	- write-back
		- data is written only to the cache
		- stays in cache until the line is to be replaced
			- faster but you must ensure there is no data loss
			- think separate cache for multiple cores, one core updates it's cache another core reads from memory
			- marked to be replaced OR requestsd by other CPU
		- main memory is temporarily inconsistent
		- Writes to cache, and later to memory
- Cache miss
	- write allocate
		- to-be written data item is read from memory into the cache
		- write performed afterwards according to the write policy
	- write-to-memory
		- modification is performed only in memory (nothing cached)

Fully associative cache
- cache lines of fixed length
- data identified by tag-field
- memory access : searching all tags for address tag

Direct mapped cache
- cache-lines with fixed length
- mapping from address to cache lines
- data identified by tag-field
- run address through hash function first


Cache design parameters
- size and set size
	- small cache -> set associative implementation with large sets
- Line length
	- spatial locality -> long cache lines
	- Cache line length influences what a good size for data structures is
		- data structures should be aligned to the length of cache lines
- write policy
	- temporal locality -> write-back
- replacement policy
- using virtual or physical addresses for taggin / indexing
![Screenshot 2024-04-14 at 16.35.17.png](../images/Screenshot%202024-04-14%20at%2016.35.17.png)

Tag
- identifies the location in memory that corresponds to the cache line
- We know the size of the cache line, so we also know what other items would be in that cache line
- Cache controller
	- determines if information requested is located in cache by checking the tags
		- if cahce hit
			- word form cache is returned and main memory is never accessed
		- cache miss
			- request is forwarded to main memory and data retrieved is stored in cache
		- hit ratio
			- ratio of hits out of total requests

cache
- tag | index | block offset
- look for stuff in parallel
- Address split into two parts to make lookup (indexing) faster
	- index
		- addresses a set of cache lines whose positions are known

physical
- has to wait for the virtual address to be translated
- expensive in case of a TLB miss

virtual addresses
- causes coherency problems, because multiple virtual addresses can map to the same physical address and mappings can change over time, requireing cache flushes

PIPT used for slow cahce

VIVT is rarely used

PIVT never used

VIPT is used for fast cache
- while lookup can start in parallel with the address translation (faster than PIPT) it uses the physical address for the last part of the lookup
- with a properly chosen size for index, it can prevent coherency problems -> depends on page size
- Should refer only to the offset within page (safe)
- limits the size of the cache

Ambiguity problem
- identical virtual addresses point to different physical addresses at different points in time

Alias problem
- different virtual addresses point to the same physical memory location

VIVT cache operations
- Context switch
	- cache mus be invalidated (and written back if write-back is used)
	- identical virtual addresses of different address spaces might (likely) reference different physical addresses
- Fork
	- the child needs a complet ecopy of the parent's address space
	- if copy operation runs in the context of the parent, special cache management is required
- Exec
	- invalidate cache to prevent ambiguities
	- not necessary to write content back as memory is overwritten anyway
- Exist
	- flush cache
- brk / sbrk
	- growing requires no action, shrinking requires (selective) cache invalidations
- Shared memory and memory mapped files -> alias problem
	- disallow
	- do not cache
	- only allow addresses that map to the same cache line (if cache is direct-mapped and uses write-allocate)
	- each frame accessible from exactly one vritual address at each point in time (requires invalidation of all alias pages in the page table)
- for unbufferred IO
	- write
		- information might still be in cahce -> write back before IO starts
	- read
		- cache must be invalidated
- Issues
	- ambiguity -> same virtual address can address different pmem in differet processes
	- aliases -> different virtual address can address same pmem in different processes
		- on modification only one cache line modified, hence


VIPT
- often used as first-level caches
- Cache management in VIPT caches
	- no ambiguities
	- no cache flush on context switch
	- shared memory / memory mapped files
		- virtual starting address must be mapped to the same cahce line
	- IO
		- cache flush required as with VIVT
- VIPT conflicts
	- data structures whose address distance is a multiple of cache size are mapped to the same cache line
- Properties
	- cache flush can be avoided most of the time
		- fast context switches, interrupt-handling and system calls
	- Deferred write-back after context switch
		- avoids write accesses (performance gain)
		- variable execution time caused by compulsory misses
- probllematic in multiprocessor systems with shared memory
	- cache size is a small multiple of page size 
	- requires to only invalidate / flush 1- 4 cache lines by cache coherency hardware
- no ambiguity but still aliases
	- ambiguity fixed because
		- appropriate tag of physical cache will not match
		- only true if tag is entire PFN
		- tag longer than in VIVT

![Screenshot 2024-04-15 at 17.49.39.png](../images/Screenshot%202024-04-15%20at%2017.49.39.png)
Types of page fault
- file backed
	- content stored in file
- zero-fill
	- generic memory area
- no access
	- illegal acces
- swap (something written to swap and modified before)

swapping not possible in inverted page tables


PIPT 
- benefits
	- Completely transparent to processor
	- no performance critical system support required (including IO)
	- SMPs with shared memory can use coherency protocol implemented in hardware
- Address translation means that a nice continuous region in virtual memory may not be nice and continuous in physical memory
- Rnadom allocation conflicts
	- contiguous virutal memory is normally mapped to arbitrary free physical pages
	- page conflicts caused by random allocation of physical memory
- Random coloring conflicts
	- consequences of random page coloring
		- cache conflicts
		- cache only partially used
		- significant variations in runtime
- PIPT conflict mitigation
	- sequential page colors for individual memory segments
	- cache partitioning
		- divide physical memory in disjoing subsets
		- all pages of a subset are mapped to the same cache partition
		- e.g.
			- all red and blue pages for operating system
			- all yellow pages for real time paplication
			- all green pages for background processes
- PIPT conflict mitigation
	- something with intel
	- Analysis of access patterns (WS analysis) and page-recoloring


Processes / threads need to communicate with one another
- Reasons
	- sharing information (file / data structure in memory)
	- computation speedup (break larger tasks into subtasks in parallel)
	- modularity (divide system into collaborating modules with clean interfaces)

IPC interprocess communication
- Allows exchanging data using
	- message passing
		- explicitly send and receive information using system calls
		- pipes
		- sockets
		- POSIX message queues
	- shared memory
		- establishes a physical memory region that multiple proceses / threads can access
		- POSIX shared memory
		- shared memory-mapped files
	- (high level abstractions -> files, databases)


Message passing
- a mechanism for processes to communicate / synchronize their actions
- facilitates 
	- send
	- receive
- Implementation of communication link
	- hardware interconnect (bus, point-to-point)
	- network interface card NIC
	- kernel memory
	- shared memory
- Types
	- direct messages
		- processes name each other explicitly when exchanging messages
			- send(pid, message)
			- receive(pid, message)
	- indirect messages
		- messages that can be sent to and received from mailboxes
		- each mailbox has a unique id
		- created by first communicating process
			- destroyed by lsat communicating process
		- processes can communicate only if they share a mailbox
		- select somehow who receives
- Sender / receiver synchronization
	- Messages may be 
		- blocking
			- Synchronous
			- blocking send has the sender block until the message is copied
				- wait until received
			- blocking receive has the receiver block until a message is available
				- wait until receive something
		- non-blocking
			- asynchronous
			- non-blocking send has the sender send the message and continue
				- send message and fuck off
			- non-blocking receive has the receiver receive a valid message or null
				- grab message or nothing if there is nothing
- Buffering
	- messages are queued using different capacities while they are in-flight
	- Zero capacity - 0 messages / no queueing
		- sender must wait for receiver (rendezvous)
		- message is transferred as soon as receiver become abailable
	- Bounded capacity - finite number and length of messages
		- sender can send before receiver waits for messages
		- sender can send while receiver still processes previous message
			- variable latency betwen send and receive
		- sender must wait if link full
			- pipe and named pipe
	- unbounded capacity
		- sender never waits
		- memory may overflow


message buffers
- best to locate in sender address space
	- if receiver -> finite memory, possibly blocking or missed
	- if kernel   -> scale poorly, provide opportunity for DDOS
	- best in sender
		- sender can reserve space for the message, and get notified once received so that he can free the memory used by the message.

POSIX message queues !
- files?

Shared memory
- Communicate through a region of shared memory
	- between processes: create shared region in one address space
	- threads naturally share address space
- every write (store operation) to that memory region is visible to all other processes
- hardware guarantees that the readers always read the most recent write
- Message passing can be implemented via a shared memory region
- Tricky (if want safe and high performance)
	- if many processes and many CPUs are involved
		- cache coherency protocol
	- if multiple writers
		- race conditions
- Assume sequential consistency
	- all memory operations occur one at a time in program order
	- ensures write atomicity
- But the compiler and the CPU re-order instruction to execution roder for more efficient execution
- memory consistency model
	- modern CPUs are generally not sequentially consistent because it would
		- complicate write buffers
		- complicate non-blocking reads (speculative prefetch)
		- make cache coherence more expensive
	- Compilers do not generate code in program order
		- re-arrange loops for better performance
		- common subexpression elimination
		- software pipelineing
	- as long as a single thread accesses a memory location at a time this is not a problem
		- if concurrent, requires proper synchronization

X86 consistency
- avoid the problem of caching
	- certain instructions such as movnt bypass the cache and can be re-orderd with other writed that do go through the cache
- lock prefix makes memory instruction atomic
	- lock instructions are totally ordered
	- other instructions cannot bere-ordered with locked ones
- Xchg instruction is always locked
- special fence instructions prevent re-orderring
	lfnece, can't be re-ordered with reads
	sfence -> write
	mfence -> read or writes

sequential consistency SC
- the result of execution is as if all operations were executed in some sequential order, and the operations of each processor occurred in the order specified by the program


POSIX shared memory !!
- map memory object to address space


Pipes
- int pipefds\[2];
- pipe(pipefds) -> initializes the pipe
- pipefds\[0] -> read end
	- char buffer\[BSIZE];
	- ssize_t nread = read(pipefds\[0], buffer, sizeof(buffer) - 1);
	- buffer\[nread] = '\0'; -> set terminal symbol at end
- pipefds\[1] -> write end
	- write(pipefds\[1], message, message lengthInBytes)

Interlocked operations
- avoid locks
- do something like compare and exchange all in one go


readers-writers problem
- model access to shared data structues
	- many threads compete to read or write the same data
	- readers only read the data set, do not perform any updates
	- writers can both read and write
- locking should reflect different semantics for reading data and for writing data
	- if no thread writes ,multiple readers may be present
	- ifa  thread writes, no other readers and writers are allowed
-  1st readers-writers problem
	- readers preference
	- no reader should have to wait if other readers are already present
	- writers can starve
- 2nd -> writers preference
	- code is the same as 1sts readers writers but separate readers and writers counts
	- readers can starve
- 3rd readers-writers problem : bounded waiting
	- no thread shall starve
	- POSIX contains readers-writers locks to address this issue
	- multiple readers but only a single writer are let into the CS
	- if readers are present whila writer tries to enter the CS, then 
		- don't let further readers in
		- block until readers finish
		- let writer in
	- service queue
		- if reader in and new reader
			- let the other reader in
		- if writer in and new reader
			- block reader until writer gone
		- if reader in and new writer
			- block writer until reader gone
		- if writer in and new writer
			- block until writer gone


Device management objectives
- abstractions
	- from details of physical devices
- uniform naming
	- Does not depend on HW details
- serialization
	- of IO operations by concurrent applications
- protection
	- of standard devices against unauthorized access
- buffering
	- if data from / to a device cannot be stored in the final destination
- error handling
	- of sporadic device errors
- virtualizing
	- physical devices via memory and time multiplexing

Block devices
- e.g.
	- disk drives
		- raw IO or file system access 
		- memory mapped file access possible
		- commands
			- read
			- write 
			- execute

Character devices
- Commands include
	- get
	- put
- Libraries layered on top allow line editing
- e.g. keyboards, mice, serial ports


Network devices
- specific communication patterns and addressing schemes require own interface
- usually addressed with socket interface
	- separates network protocol from network operation

IO hardware
- canonical device interface
	- status register
	- control register
	- data-in register
	- data-out register
- devices are referenced by addresses
	- direct IO instructions
	- memory-mapped IO
	- port mapped IO
		- IO devices have a separate address space from general memory either accomplished by an extra IO pin on the CPU's physical interface or an entire bus dedicated to IO.

Polling vs. interrupt driven IO
- programmed IO
	- thread is busy-waiting for the IO operation
	- kernel thread is polling the state of an IO devcie

Polling vs. interrupts
- fast device -> better to spin than take the interrupt overhead
- device time unknown
	- hybrid approach (spin, then use interrupts)
- Flood of interrupts arrive
	- can lead to livelock (always handling interrupts)
	- better to ignore interrupts while make some progress handling them
- interrupt coalescing (batch together several interrupts)


Direct memory access (DMA
- DMA module controls exchange of data between main memory and IO device
- processor interrupted after entire block has been transferred
- bypasses CPU to transfer data directly between IO device and memory


Interrupt driven IO
- IO command is issued 
- processor continues executing instructions
- IO device sends an interrupt when IO command is done


Handling interrupts
- save registers not already saved by hardware interrupt mechanism
- set up context (address space) for interrupt service procedure
	- typically, hanlder runs in the context of the currently running process / task
		- no expensive context switch
- Set up stack for interrupt service procedure
	- handler usually runs on the kernel stack of the current process / kernel level thread
	- handler cannot block, otherwise the unlucky interrupted process / kernel thread would also be blocked, might lead to starvation or even to a deadlock
- Acknowledge / mask interrupt controller, thus re-enable other interrupts
- run interrupt service procedure
	- acknowledge interrupt at device level
	- figure out what caused the interrupt
	- if needed, signals the blocked device driver
- in some cases have to wake up a higher priority process / KLT
	- potentially shcedule another process/KLT
	- set up MMU context for process to run next
- load new / orignal process' register
- return from interrupt, start running new / oringal process
![Screenshot 2024-04-14 at 21.03.58.png](../images/Screenshot%202024-04-14%20at%2021.03.58.png)


Functions of kernel IO subsystem
- device reservation - provides exclusive access to a device
	- system calls for allocation and deallocation
- Protection
	- IO must be performed via system calls
		- memory mapped and IO port memory locations must be protected
- Spooling
	- hold output for a device, if device can serve only one request at a time
- uniform kernel interface for device code
	- drivers use a defined interface to kernel service
	- allows kernel to evolve without breaking device drivers
- Request scheduling
	- some IO request ordering via per-device queue
	- some OSs try fairness
- Buffering
	- store data in memory while transferring between devices
	- to cope with
		- device speed mismatch
		- device transfer size mismatch
	- maintain copy semantics
- Error handling and reporting
	- OS can recover from errors
		- disk read
		- device unavailable
		- transient write failures
	- error reporting to upper levels 
		- all errors driver cannot resolve


Device driver
- after issuing the command to device, it either
	- completes immediately and the driver simply returns to the caller or
	- process request and driver blocks waiting for an IO interrupt signal
- Drivers are reentrant as they can be called by another process while a process is already blocked in the driver

reentrant
- code that can be executed by more than one thread at the same time
- manages concurrency using sync primitives


Lifecycle of IO request
![Screenshot 2024-04-14 at 21.14.03.png](../images/Screenshot%202024-04-14%20at%2021.14.03.png)


![Screenshot 2024-04-14 at 21.23.57.png](../images/Screenshot%202024-04-14%20at%2021.23.57.png)




Explain the function of the file system
Describe the interface to file systems
discuss file-system design aspecsts
- access methods
- file sharing 
- file locking

File types
- data
	- text
	- binary 
	- dedicated file formats for specific purposes
- program


File systems
- OS may support multiple file systems
	- of same or multiple differnt types
	- All file systems are typically bound into a single namespace
- often hierarchichal as a rooted tree
	- Internal node = directory (mount point)
- Files are located on disk
	- Complex physical devices
		- OS hides complexity from higher level software
			- low-level device control
			- high-level abstractions
		- May provide different levels of disk access to different clients (Applications)

Different levels of disk access
- physical disk (surface, cylinder, sector)
- logical disk = partition (disk block number)
- logical volume = multiple partitions (volume block number)
- logical file (file block ,record, byte number)

File
- a collection of related information
- has a set of attributes (meta data) (different between OS and FS)
	- name, identifier
	- type
	- location (physical address of a file on device)
	- size (number of bytes or number of blocks)
	- protection (permission)

File structure
- None
	- sequence of words, bytes
- simple record structure
	- lines
	- fixed length
	- variable length
- Complex structures
	- formatted document
	- relocatable executable object

Three kinds of file (from OS)
- byte sequence 
	- provides maximal flexibility
- record sequence
	- often fixed sized records
- tree 
	- sometimes variable sized records

File types
- regular files
	- executable, dll, object, source, text
- Special files
	- directory, device (character, block) links
- file's type can be encoded
	- in inode
	- in name
	- in content (magic number or initial character)


Abstract file operations
- create
- write
- read
- reposition
- delete
- truncate
- open(fi)
	- search directory structure on disk for entry Fi, and move its meta data to memory
- close(fi)
	- move cached meta data of entry Fi in memory to directory structure on disk


File system interface
- File directory service
	- resolves filename
	- enhances usage of files
	- controls access
	- allows sharing
- file storage service
	- hides specifics of storage media
	- preserves files even in case of hardware or software failure


Goals of file management
- provide a convenient naming scheme for files
- provide uniform IO support for a variety of storage device types
- provide standardized set of IO interface functions
- minimize or eliminate loss or corruption of data
- provide IO support and access control for multiple users
- enhance system administraction
- provide acceptable performance


Other file attributes
- owner
- read-only flag
- hidden flag (display in listings)
- system flag (system file)
- archive flag (needs to be backed up?)
- ASCII / Binary bit (0 ascii, 1 binary)
- random access flag (0 sequential access only)
- termpoary flag (1 delete file on process exit)
- lock flags (0 unlocked)
- creation time
- time of last access
- time of last change
- maxium size


Open files
- meta data to manage
	- file pointer 
		- pointer to last read / write location, per process that has the file opened
	- access rights
		- per-process / task access mode information (read / write)
	- file-open count
		- counter of number of times a file is opened -> allows removal of data from open-file table when last process closes
	- disk location
		- cache of data access information

Plain file
- a sequence of bytes (with possible gaps) typically located on a disk
- characteristics
	- you can randomly acces any byte within an unstructured file if you have positioned its file pointer appropriately
- problem
	- disks cannot access bytes; only blocks
	- solution
		- buffer file blocks or entire file (mmap) within main memory

Directories
- goals
	- naming convenient to users
		- two users can have same name for differnt files
		- the same file can have several different names
	- grouping
		- logical grouping of files by properties
	- efficiency fast operation
- Operations
	- create file
	- delete file
	- rename file
	- traverse file system
	- list a directory
	- search for a file
- what
	- a node in an FS owned by an authorized subject, containing information about (some or all) files of the FS
	- both directories and files reside on disk

Filesystem structure
- collection of directories and ilfes establish a hierarchichal FS structure
- principle structure of modern FS is a rooted tree
	- pahtnames help unambiguously identify files
	- provides mappings between file names -> files
- on UNIX systems
	- single uniform FS tree
		- different types of file systems are mounted into uniform tree

Single-level directory
- a single directory for all users
	- naming problems
	- grouping problems

Two-level directory
- separate directory for each user
- master file directory, then a user file directory
	- path name 
	- can have the same file name for differetn user
	- efficient searching
	- no grouping capability

Tree-structured directories
- efficient searching & grouping capability
- unambiguous file names via pathnames

Working directory
- current directiory cwd
	- files is references via shorter relative pathname
	- cwd belongs to a process' task's exeuction environment
	- initial cwd is often called home
- relative vs. absolute pathnames
	- absolute pthname
		- path from root of FS to file
	- relative pathname
		- path from current working directory
		- . -> current
		- .. -> parent
	- implies improved portability
		- can send root of tree to other places, and references still work

UNIX directory operations
- opendir
- closedir
- readdir
- mkdir
- rmdir


UNIX link
- direct access to a file without navigation
- UNIX hard link
	- another name for the same file or inode
	- file is only deleted if last hardlink has been deleted (refcoutn in inode = 0)
	- invalid links are not possible
	- must be in the same file system
- symbolic link ln -s filename linkname
	- a new linkname with a link to a file with name filename whose file might be currently not mounted or not even exist
- results in acyclic-grpah FS structure
	- links cannot point to directories or else cycles would exist

Access rights
- execute
	- user can load and execute a program but cannot copy it
- read
	- user can read the file for any purpose
- append
	- user can only add data to af ile but cannot modify or delete any data in the file
- updaing
	- user can modify, delete and add to file's data, including creating the file, rewriting it, removing all or some data from the file
- changing protection
	- user can cahnge access rights gratnted to other users
- deletion
	- user can delete the fiel
- owner
	- has all rights
	- may grant rights to other users following classes of users

Shortcomincs of UNIX access rights
- three user (subject) categories is not enough
- UNIX ACL
	- a list bound to a file f containing all indvididual suubjects & their individual permissions how to access this file f
	- more control


Concurrent access to files
- some OSs provide mechanisms for users to manage concurrent access to files
- applications can lock
	- entire file for updating file
	- individual records for updating
- exclusive or shared
	exclusive - writer lock
	shared - multiple readers allowed
- mandatory or advisory
	- mandatory -> acess is denied depending on locks held and requested
	- advisory  -> processes can find status of locks and decide what to do

Disk structure
- disk can be subdivided into partitions (minidisks / slices)


Disk partitions
- can be used
	- raw (without file system)
	- formatted with file system (FS)
	- volume
		- an entity containing FS
	- many general-purpose FSs exist and can co-exist on the same volume


Implementing FS on disk
- first sector of disk = MBR
	- boot info (BIOS reads and executes MBR)
	- disk partition info
	- sector 0 is volume boot record
- FS specific internal organization within partition
- Disk organized into fixed-sized blocks'
	- data region
		- for user data and metadata
			- which logical blocking belongs to which file, in what order
			- metadata for each file
				- size
				- owner
				- access rights
				- access / modification time stamps
				- which blocks are free for the next allocation


File metadata
- attributes
	- size
	- owner
	- access rights
	- access / modification time stamps
	- which blocks are free for the next allocation
- typical data structures
	- inodes (index nodes)
		- fixed-size multiple inodes per block
		- allocation tracking 
			- free list 
			- data bitmap
			- inode bitmap
		- superblock
			- magic number
			- file system type id
			- FS info
				- number of data and inode blocks


Allocation policies
- how to allocate data blocks for a new file
- preallocation
	- need to know maximum size of a file at creation time
	- difficult to reliably estimate maximum size of af ile
	- users tend to overestimate file size, just to avoid running out of space
- dynamic allocation
	- allocate in pieces as needed

Fragment size (block size)
- tradeoffs
	- contiguity -> speedup for sequential access
	- many small fragments -> larger tables needed to manage free stoarge management as well as to support access to files
	- larger fragments help to improve data transfer
	- fixed-size fragments simplify reallocation of space
	- variable-size fragments minimize internal fragmentation but can lead to external fragmentation

3 implementations of files
- contiguous
	- array of n contiguous logical blocks reserved per file
	- minimum meta data per entry in FAT / directory
		- starting block address
		- size of file
	- results in scattered disk
	- use periodic compaction to overcome external fragmentation
- chained (linked)
	- linked list of logical file blocks for each file
		- each file block has a pointer to next file block
		- if stored in block, amount of data space per block is no longer a power of two
			- consequences for external fragmentation (buddy allocaion not possible)
		- last block contains nil pointer
	- FAT (directory) contains address of first file block
	- no external fragmentation
		- any free block can be added to the chain
	- only suitable for sequential files
		- no easy backwards seek
	- no accommodation of the principle of disk locality
		- file blocks will end up scattered accross the disk
		- run a defragmentation utility to improve situation
	- Using RAm
		- seperate file allocation table with linked list info in ram for faster access
		- avoid disk access when searching for block
		- entire block is available for user data
		- table gets far too large for modern disks
		- similar to an inverted page table, one entry per disk block
- indexed
	- file allocation table contains an index table for each file
		- fixed size array of fragment pointers
		- fixed block fragments
		- variable block fragments
	- allocate space for pointers at file creation time
	- one node (the inode) points to all data node locations 
	- analysis
		- supports sequential and random access to a file
		- fragments 
			- block sized (no external fragmentatino) large overhead for unneeded pointers 
	- varialbe sized
		- improves contiguity
		- reduces index size

Inode
- mode
- owners
- timestamps
- size block counts -> data blocks
- direct blocks -> inodes with pinters to data blocks
- single indirect -> inodes pointing to inodes containing data blocks
- double indirect -> inodes ...

![Screenshot 2024-04-14 at 22.22.57.png](../images/Screenshot%202024-04-14%20at%2022.22.57.png)



Handling long file names in directory entrries
- in-line   -> in the directory itself
- in a heap -> in inode, pointer to filename in heap

FAT32 linear directoyr lookup
- fixed size (32byte) directory table entries
	- 8 bit filename
	- 3 byte file extension
	- attributes
	- special fileanames
		- 00h -> end of list
		- e5h -> free entry (deleted file)

directory lookup
- linear
	- just search through all directories
- hashing
	- hash file name to an inode
	- extendible hasing (based on Fagin's algorithm)
		- hash table with 2^k buckets
		- k lowest bits of file name hash used to select bucket
		- block full: split into two (increase k by one if necessary)
	- fast and relativley simple
	- not as efficient as trees for very large directories
- Tree structure
	- sort files by name
	- store directory entries in a B-tree structure
	- create / delete / search in that B-tree
	- efficient for a large number of files per directory
	- cons
		- complex
		- not efficient for small number of files

Buffer cache

write-behind
- may lead to
	- data losses in case of system crash or power loss
		- force all dirty buffers to disk with fsync()
	- inconsistent state of FS
		- use journaling (write-ahead logging)


rename() on file is implemented atomically (so as to not lose any files)

Virtual file systems
- an object oriented way of implementing file systems
- Allows the same system call interface (API) to be used for different types of file systems
- API is for the VFS interface, rather than any specific type of file system
- Allows mounting different file systems onto the same file system interface
- ![Screenshot 2024-04-14 at 23.19.11.png](../images/Screenshot%202024-04-14%20at%2023.19.11.png)


Logical file system
- can consists of different physical file systems
- A file system can be mounted at any place within another file system
- mount / unmount the OS manages a mount table supporting the resolution of path name crossing file systems

![Screenshot 2024-04-14 at 23.20.42.png](../images/Screenshot%202024-04-14%20at%2023.20.42.png)

Inode table is stored in a buffer

Unix inode
- mode 
	- file type, protection bits, setuid, setgid bits
- nlinks
	- number of directory entries pointing to this i-node
- uid
	- UID of the file owner
- gid
	- GID of the file owner
- size
	- file size in bytes
- addr
	- address of first 10 disk blocks, then 3 indirect blocks
- gen
	- gernation number (incremented every time i-node is reused)
- atime
	- time the file was last accessed
- mtime
	- time the file was last modified
- ctime
	- time the i-node was last changed


BSD FFS (Fast file system)
- use a larger block size 4KiB
	- allow large blocks to be chopped into 2, 4, or 8 sub blocks
	- used for little files and pieces at the end of files
	- as the file grows, continue to allocate sub-blocks
	- if 4KiB reached, copy sub-blocks to a full 4KiB block
- use bitmap instead of free list
	- try to allocate more contigusly
	- 10% free space reserve for sysadmin
- optimizatinos to better match disk characteristics
	- cylinder grouops for exploiting locality
	- data and meta data in same cylinder group
	- items of one directory in same or nearby cylinder groups

FFS / EXT2 directory
- directory entry needs three elements
	- inode number (index to a table of inodes)
	- length of dir-entry (variable length of file names)
	- entry type
	- file name length
	- file name (up to 255 characters)
- each directory contains at least two entries
	- .
	- ..
- FFS offers tree like structure

Inode table
- superblock
	- generic information about the file system (type / version, blocksize, number of inodes, etc.)
- i-bmap
	- free inode bitmap
- d-bmap
	- free data block bitmap

Journaling file systems
- record each update to the file system as a transaction
- all transactions are written to a log
	- a transaction is considerd committed once it is written to the log
	- however, the file sysetm may not yet be updated
- transactions in the log are asynchronously written to the file system
	- when the file system iss modified, the transaction is removed from the log
- if the file system crashes, all remaining transactions in the log must still be performed.


Log-structured file system
- use disk as circular buffer
- write all updates, including inodes, meta data and data to end of log
	- have all writs initially bufferred in memory
	- periodically write these within 1 segment (1 MB)
	- when file opened locate i-node then find blocks
- from other end clear all data, no longer used
- all writes go to an append only log
- avoid seeks at all costs
- inode map alltaf fremst


FAT
- file allocation table
- two types of clusters
	- data clusters containing file contents
	- directory clusters containing directory structures for the file system
		- file system metadata for all files
		- file names
		- time stamps
		- starting cluster for all files
- root directory at beginning of disk
	- first set of clusters
- FAT table
	- in a special location at beginning of list
	- a map of all clusters in the system by cells
	- 0 unallocated
	- fff7 -> bad cluster
	- fff8 end of file
	- all other values meaning that the block is allocated

Hard disk
- provide
	- cost efficiency
	- endurable -> nearly infinite reads and writes
	- reliable
	- large
- made
	- stack of magnetic platters spinning at 3600 - 15000 RPm
	- Disk arm
		- arm rotates around pivot
		- all arms move together
		- arms contain disk heads, one for each recording surface
		- Heads 
			- read and write data to platter
			- hovers above disk
	- Servo codes
		- position disk on data
	- landing zone
		- when device motor is offline the head touches disk in a special landing zone without data
- Magnetic storage
	- Longitudinal Magnetic recording (LMR)
		- early recording mode, similar to audio tape
	- perpendicular magnetic recording (PMR)
		- perpendicular to traditional magnetic recording
		- up to 3x higher density
	- Shingled magnetic recording
		- writes new tracks that overlap previously written magnetic tracks
			- higher density
		- combined with large caches to minimize reduced write speed
	- Heat-assisted magnetic recording (HAMR)
		- temporarily heating the disk material during writing -> increases density even further
- storage
	- platter
		- divided into tracks
		- a stack of tarcks of fixed raidus is a cylinder
	- one head active at a time
		- hard to keep multiple heads exactly aligned
		- disks usually have one set of read-write circuitry
	- access time has two major components
		- seek time is the time for the disk to move the heads to the cylinder containing desired sector
		- rotational delay is the additional time waiting for disk to rotate the desired sector to the disk head
	- Disk positioning
		- move head to specific track and keep it there
			- needs to resists phyical shocks and imperfect track positioning
		- seek phases
			- speedup -> accelerate arm to max speed or half way point
			- coast -> at max speed (for long seeks)
			- slowdown -> stop arm near destination
			- settle -> adjust head to actual desired track
		- very short seeks -> settle time
		- short seeks -> speedup
	- Disk keeps table of pibot motor power
		- maps seek distance to power and time
		- disk interpolates over entries in table
		- table set by periodic thermal recalibartion
		- 500 ms recalibration every 25 minutes
- Sectors
	- disk interface presents linear array of sectors (LBA)
		- 512 bytes written atomically
		- OS doesn't know logical LBA to physical sector mapping
			- larger logical sector number differencemeans larger seek
			- hihgly non-lienar relationship and depends on zone
			- OS has no info on rotaitional positions 
	- disk maps logical sector number to physical sector (CHS
		- zoning -> put more sectors on longer tracks
		- track skewing -> sector 0 pos. varies by track to improve sequential access speed
		- sparing -> flawed sectors remapped to spare sectors

Disk interface
- controls hardware, mediates access
- Serial interface SATA / SAS
- features
	- command queueing : give disk multiple requests
		- disks can schedule using rotational info
		- similar to CPU scheduling
	- read ahead into disk cache
		- cahching tracks to speed up sequential reads
		- otherwise next block as to wait for a hole revolution
	- write caching
		- but data not stable - not suitable for all requests

Disk performane
- placement & ordering of reqeusts is a huge issue
	- sequential IO is much faster than random
	- long seeks much slower than short ones
- try to achieve contiguous accesses where possible
	- make big chunks of individual files contiguous
- try to order requests to minimize seek times
	- OS can only do this if it has multiple requests to order
	- disks show high degree of internal concurrency
	- high-performance apps try to maximize IO concurrency


SSD
- no moving parts
	- remembers data by storing charge
	- lower power consumtption and heat
	- no mechanical seek times to worry about
	- blocks wear out
		- 10.000 multi-level cell erasure
		- 100.000 single level cell erasures
	- requires flash translation layer FTL to provide wear leveling so repeteated writes to logical blocks don't weakr out physical block
	- FTL can impact performance
	- random writes are very expensive
- limited durability
- has some amount of pages
- blocks contain some amount of pages
	- SLC large pages
	- MCL small pages
- Blocks partitioned into planes
	- all planes contend for same package pins
	- but can access their blocks in parallel to overlap latencies
- must erase whole block before programming
	- set all bits to 1 (expensive 2msec)
	- programming pre-erased blocks is much faster 200 - 800 microseconds

Multi-level cell
- containing many cells


Performance optimization for ssd
- Spare block
	- ssd controller always keeps a set of erased spare blocks
	- on an ssd block re-write
		- spare ssd block is susedfor writing, the old ssd block is marked for erasure
	- erasure happens in background if device is idle
	- (can tolerate a moderate modificatioun rate without erase penalty)
	- trim
		- OS tells the SSD about deleted logical blocks (don't have to be copied in case of SSD block re-write)
		- unused logical blocks increase the pool of spare SSD blocks after garabage collection

Imrpove disk IO
- use multiple disks to parallelize disk IO
- provide a better disk availability
- instead of 1 single large expensive disk use redunadnt array of independent disks
- RAID
	- improve performance and reliabity of storage system by storing redundant data
		- mirroring or shadowing keeps duplicate of each disk
		- bit/byte/block interleaved parity used much less redundancy

RAID 2 - hamming code
RAID3 - byte / word-interleaved parity


RAID 0 + 1
- mirror of stripes
- fails if 2 drives in 2 stripes fail

RAID 1 + 0
- fails if 2 drives in same group fail
- lower proability of failure than raid 01
- ![Screenshot 2024-04-15 at 13.03.22.png](../images/Screenshot%202024-04-15%20at%2013.03.22.png)







Privileged operations
- instructions that control and mange the system as a whole and should only be performed by the operating system
	- enabling / disabling interrupts
	- settign current address space CR3
	- halt the processor
- Kernel of operating system invoked
	- interrupts
	- exceptions 
	- system calls

Anatomy of system call
- OS configures trap instruction
- program puts arguments on stack / register
- program puts sytem call number on stack / regiser
	- identifies the requested service
- program executes trap instruction
- CPU switches to privileged mode and jumps to sytem service dispatcher
- dispatcher copies arguments on kernel stack and performs various checks
- find service routine for syscall number and calls it
- system service routine checks arguments and performs service
- return to dispatcher and call to system exit instruction
- programa continues in user space


Segments of a program
- code
- RONLY data
- Data
- BSS
- (NOT heap and stack -> process)

Fork
- copy of process that shares most of the resources with its parent
	- address spaceopen file table'


Scheduling goals
- throughput
- turnaround time
- CPU utilization
- waiting time
- response time

Scheduling policies
- FCFS
- SJF
- PSJF
- RR
- Priority scheduling
- multi-level feedback queue
- Lottery scheduling

Difference between process and thread
- processes are containers for the execution of a program and hold many of the necessary resrouces (address space, handles tables)
- threads execute code. Depending on the context a process is often also considered to contain at least one implicit thread

Kernel-level threads
kernel-mode threads
user-level threads


Scheduling models
- one-to-one -> KLT only (OS managed threads)
- many-to-one -> OS only knows one thread, that thread manages ULT
- many-to-many (hybrid) -> OS knows some ULT but not all, can mix two

Virtual to physical mapping techniques
- base and limit register
- segmentation
- paging

What identifies an address space with segmentation
- segment-table base register (STBR)
- segment-table length register (STLR)
- info stored
	- base address
	- length
	- protection

Advanced memory allocators
- buddy allocator
- slab allocator

When can compaction be used - only when there's an extra layer of indirection between the address that we give away (pointers) and the actual position of allocated memory blocks



MMU
- hardware support for virtual to physical address translation and memory protection

TLB
- address translation cache to reduce memory accesses due to address translation
- hardware managed 
	- on TLB miss MMU resolves situation by walking memory mapping structure
- software managed
	- invoke OS

Page
- unit of translation for paging-based memory management
- virutal address space is built from apges
- pages in physical address space are called frames (must have same size)

What identifies an address space with pageing
- page table -> at a specified physical addres sin ram stored on CR3 register

page tables
- linear page talbe
- multi-level page table
- linear inverted page table
- hashed inverted page table


PTE
- valid / present bit
- page frame number
- read / write bit
- user / kernel bit
- caching bit
- accessed bit
- dirty bit

tradeoff between small and large pages
- large pages
	- more memory wasted due to internal fragmentation
	- fewer bits needed for page / frame number (more bits in offset)
	- fewer page tables / fewer PTEs
	- more data to be loaded from disk to make page valid

Page fault
- MMu cannot translate a virtual to a physical address or detected an illegal access and invokes the operating system to handle the situation
- also TLB miss

Page fetch policies
- demand-paing
- pre-paging

page replacement policies
- FIFO
- optimal page replacement
- LRU
- clock
- random


IPC
- shared memory
- message passing
	- pipes
	- message queues

sender receiver sync
- blocking (sync)
- non-blocking (async)

Messages need to be buffered when using async communication
- sender process user memory
- receiver process user memory
- kernel memory

Requirements for valid synchronizatoin
- exlusiveness
- progress
- bounded waiting

Synchronization primitives
- spinlock
- counting semaphore
- binary semaphore / mutex
- condition variable
- reader-writer lock
- futex

bardware support for syn
- atomic operations

deadlock conditions
- mutual exclusion
- hold and wait
- no preemption
- circular wait

how to address disk
- via sector number LBA
- internally translated to a physical sector by hard disk CHS

ssd
- rewriting data is slower than writing it
	- cannot write a 1 or 0 anywhere in the memory
	- a bit can only be set to 0
	- rewriting can only be done on large blocks (64 - 128 pages)
- rewriting
	- read entire block
	- erase it 
	- write modified page as well as unmodified pages in another block or back in the same block
- helps
	- spare blocks
	- trim command

File desriptor
- an integer representing an instance of an open file


Access control mechanisms
- UNIX access rights
- access control lists ACLs

Disk block allocation
- Contiguous allocation
- chained allocation
- linked-list allocation and file allocation table FAT
- indexed allocation

inode
- file size
- abstract file type (sl, directory, block, charaacter, plain file)
- access rights
- timestamps 
- ordered list of data block numbers

Directories
- a file containing entreis for each file in the directory
- entry contains
	- name of file 
	- link to inode


Virtual file system
- provides a unified interface for different file systems
- same tools can be used without taking care of the type of the file system
- special FS features are only accessible through narrow interface 



File system cache - buffer cache
- stores recently received data from disk

read-ahead
- benefits
	- good performance on sequential or predictable file access
	- improved disk throughput if files reside in successive disk blocks
- cons
	- wasted bandwidth if failed

Cache-based side channels
Spectre
- branch prediction
- Branch prediction lets CPU run code that would not otherwise be run
Meltdown
- out of order execution
- allows access to pages that are marked user in page table


MMAP
- mapped in user space so needs no buffer
- doesn't read anything from disk when setup (or pre-fetch)
- sets up page entries that tell the system to read data form disk fiel when vaddr is accessed
- data mapped directly in user space so no copying memory from kernel memory to application memory
	- faster as a result of the time taken to do this (regularly)
- results in more page faults (but can implement read ahead / pre-fetching)


Primary IO models
- polling
	- process polls to see if read is done
	- fetches directly from device register itself
- interrupt driven
	- once interrupt comes CPU fetches data from device register and places in main memory
- DMA
	- provided with physical location in PMEM, sends interrupt once finished

Devices
- character
	- serial character oriented devices
	- e.g. keyboard
- block
	- internally update blocks of data
	- must support seeking to arbitrary locations (linux)
	- e.g. disk
- network


Contiguous allocation
- store only start and size
	- limited to said size (cannot changecompaction possible but expensive
	- fast sequential reads

Linked allocation
- no longer need to occupy contiguous blocks
- block contains pointer to next block
- only sequential access (no random)
- if a pointer is corrupted, everything is fucked

FAT - file allocation table
- linked allocation but store list info separately
	- in the FAT itself
- entire list has to be walked to find specific byte offset in file
- size depends on size of hard disk.