---
title: "Programación concurrente - fundamentos"
---

# Concurrent Programming

Recopilación de artículos de Wikipedia on
Answers.com realizada por el profesor Luis
Bengochea para su uso como material de
consulta de la asignatura de Programación
Avanzada.
These articles are licensed under the Creative Commons
Attribution/Share-Alike License.
Concurrent Programming
Contenido
Concurrent programming 6
Concurrent interaction and communication 6
Coordinating access to resources 7
Advantages 7
Concurrent programming languages 8
Models of concurrency 10
See also 10
References 10
Further reading 10
External links 11
Synchronization 11
Process synchronization 11
See 12
Data synchronization 12
Mathematical foundations 12
External links 12
Critical section 13
Application Level Critical Sections 14
Kernel Level Critical Sections 15
See also 16
External links 16
Mutual exclusion 17
Enforcing mutual exclusion 17
Hardware solutions 17
Software solutions 18
Advanced mutual exclusion 18
Further reading 19
See also 19
External links 19
Lock 20
Types 20
Granularity 21
Database locks 22
The problems with locks 23
Language support 24
See also 24
References 25
Monitor 26
Mutual exclusion 26
Waiting and signaling 27
Blocking condition variables 28
Nonblocking condition variables 31
Implicit condition variable monitors 33
Implicit signaling 34
History 34
See also 35
Bibliography 35
External links 35
Notes 36
Semaphore 37
Library analogy 37
Important observations 38
Semantics and Implementation 38
Example: Producer/Consumer Problem 39
Function name etymology 40
Semaphore vs mutex 40
Current usage 40
See also 41
Notes and references 41
Message passing 42
Overview 42
Message passing systems and models 42
Synchronous versus asynchronous message passing 43
Message passing versus calling 43
Message passing and locks 44
Examples of message passing style 45
Influences on other programming models 45
See also 45
References 46
External links 46
Further reading 46
Tuple space 47
Object Spaces 47
JavaSpaces 48
Example usage 48
Implementations 49
Books 50
Interviews 50
Articles 50
References 51
See also 51
Sources 52
External links 52
Atomicity 53
Primitive atomic instructions 53
High-level atomic operations 54
Example atomic operation 55
Non-atomic 55
Compare-and-swap 55
Locking 56
History of linearizability 56
Definition of linearizability 57
Linearizability versus serializability 57
Linearization points 58
Strict consistency 58
See also 58
References 59
Concurrency control 60
Concurrency control in databases 60
Database transaction and the ACID rules 61
Why is concurrency control needed? 62
Concurrency control mechanisms 62
See also 66
References 66
Concurrency control in operating systems 66
See also 67
References 67
Mutually exclusive events 68
Logic 68
Probability 68
Statistics 69
See also 69
Notes 70
References 70
Dining philosophers problem 71
Problem 71
Issues 71
Solutions 72
Conductor solution 72
Resource hierarchy solution 73
Monitor solution 73
Chandy / Misra solution 74
Example solution 75
See also 79
References 79
External links 80
Deadlock 81
Examples 82
Necessary conditions 82
Prevention 83
Avoidance 83
Detection 84
Distributed deadlock 84
Livelock 86
See also 87
References 87
Further reading 87
External links 88

## Concurrent programming

Concurrent computing is a form of computing in which programs are designed as
collections of interacting computational processes that may be executed in parallel.[1]
Concurrent programs can be executed sequentially on a single processor by interleaving
the execution steps of each computational process, or executed in parallel by assigning
each computational process to one of a set of processors that may be close or distributed
across a network. The main challenges in designing concurrent programs are ensuring
the correct sequencing of the interactions or communications between different
computational processes, and coordinating access to resources that are shared among
processes.[1] A number of different methods can be used to implement concurrent
programs, such as implementing each computational process as an operating system
process, or implementing the computational processes as a set of threads within a single
operating system process.
Pioneers in the field of concurrent computing include Edsger Dijkstra, Per Brinch
Hansen, and C.A.R. Hoare.
**Contents**
- 1 Concurrent interaction and communication
- 2 Coordinating access to resources
- 3 Advantages
- 4 Concurrent programming languages
- 5 Models of concurrency
- 6 See also
- 7 References
- 8 Further reading
- 9 External links

### Concurrent interaction and communication

In some concurrent computing systems, communication between the concurrent
components is hidden from the programmer ( e.g., by using futures), while in others it
must be handled explicitly. Explicit communication can be divided into two classes:
Shared memory communication
Concurrent components communicate by altering the contents of shared memory
locations ( exemplified by Java and C#). This style of concurrent programming usually
requires the application of some form of locking ( e.g., mutexes, semaphores, or
monitors) to coordinate between threads.
Message passing communication
Concurrent components communicate by exchanging messages ( exemplified by Erlang
and occam). The exchange of messages may be carried out asynchronously, or may use
a rendezvous style in which the sender blocks until the message is received.
Asynchronous message passing may be reliable or unreliable ( sometimes referred to
as "send and pray"). Message-passing concurrency tends to be far easier to reason
about than shared-memory concurrency, and is typically considered a more robust
form of concurrent programming. A wide variety of mathematical theories for
understanding and analyzing message-passing systems are available, including the
Actor model, and various process calculi. Message passing can be efficiently
implemented on symmetric multiprocessors, with or without shared coherent
memory.
Shared memory and message passing concurrency have different performance
characteristics; typically ( although not always), the per-process memory overhead and
task switching overhead is lower in a message passing system, but the overhead of
message passing itself is greater than for a procedure call. These differences are often
overwhelmed by other performance factors.

### Coordinating access to resources

One of the major issues in concurrent computing is preventing concurrent processes
from interfering with each other. For example, consider the following algorithm for
making withdrawals from a checking account represented by the shared resource
balance:

```

1 bool withdraw ( int withdrawal )
2 {
3 if ( balance >= withdrawal )
4 {
5 balance -= withdrawal;
6 return true;
7 }
8 return false;
9 }

```

Suppose balance=500, and two concurrent processes make the calls withdraw ( 300)
and withdraw ( 350). If line 3 in both operations executes before line 5 both operations
will find that balance > withdrawal evaluates to true, and execution will proceed to
subtracting the withdrawal amount. However, since both processes perform their
withdrawals, the total amount withdrawn will end up being more than the original
balance. These sorts of problems with shared resources require the use of concurrency
control, or non-blocking algorithms.
Because concurrent systems rely on the use of shared resources ( including
communication media), concurrent computing in general requires the use of some form
of arbiter somewhere in the implementation to mediate access to these resources.
Unfortunately, while many solutions exist to the problem of a conflict over one
resource, many of those "solutions" have their own concurrency problems such as
deadlock when more than one resource is involved.

### Advantages

This section does not cite any references or sources.
Please help improve this article by adding citations to reliable sources. Unsourced material
may be challenged and removed. ( December 2006)
 Increased application throughput - parallel execution of a concurrent program allows
the number of tasks completed in certain time period to increase.
 High responsiveness for input/output - input/output-intensive applications mostly wait
for input or output operations to complete. Concurrent programming allows the time
that would be spent waiting to be used for another task.
 More appropriate program structure - some problems and problem domains are well-
suited to representation as concurrent tasks or processes.

### Concurrent programming languages

Concurrent programming languages are programming languages that use language
constructs for concurrency. These constructs may involve multi-threading, support for
distributed computing, message passing, shared resources ( including shared memory) or
futures ( known also as promises). Such languages are sometimes described as
Concurrency Oriented Languages or Concurrency Oriented Programming Languages
( COPL).[2]
Today, the most commonly used programming languages that have specific constructs
for concurrency are Java and C#. Both of these languages fundamentally use a shared-
memory concurrency model, with locking provided by monitors ( although message-
passing models can and have been implemented on top of the underlying shared-
memory model). Of the languages that use a message-passing concurrency model,
Erlang is probably the most widely used in industry at present.[citation needed]
Many concurrent programming languages have been developed more as research
languages ( e.g. Pict) rather than as languages for production use. However, languages
such as Erlang, Limbo, and occam have seen industrial use at various times in the last
20 years. Languages in which concurrency plays an important role include:
 ActorScript – theoretical purely actor-based language defined in terms of itself
 Ada
 Afnix – concurrent access to data is protected automatically ( previously called Aleph,
but unrelated to Alef)
 Alef – concurrent language with threads and message passing, used for systems
programming in early versions of Plan 9 from Bell Labs
 Alice – extension to Standard ML, adds support for concurrency via futures.
 Ateji PX – an extension to Java with parallel primitives inspired from pi-calculus
 Axum – domain specific concurrent programming language, based on the Actor model
and on the .NET Common Language Runtime using a C-like syntax.
 Chapel – a parallel programming language being developed by Cray Inc.
 Charm++ – C++-like language for thousands of processors.
 Cilk – a concurrent C
 Cω – C Omega, a research language extending C#, uses asynchronous communication
 Clojure – a modern Lisp targeting the JVM
 Concurrent Clean – a functional programming language, similar to Haskell
 Concurrent Haskell – lazy, pure functional language operating concurrent processes on
shared memory
 Concurrent ML – a concurrent extension of Standard ML
 Concurrent Pascal – by Per Brinch Hansen
 Curry
 E – uses promises, ensures deadlocks cannot occur
 Eiffel – through its SCOOP mechanism based on the concepts of Design by Contract
 Erlang – uses asynchronous message passing with nothing shared
 Faust – Realtime functional programming language for signal processing. The Faust
compiler provides automatic parallelization using either OpenMP or a specific work-
stealing scheduler.
 Go – systems programming language with explicit support for concurrent
programming
 Io – actor-based concurrency
 Janus features distinct "askers" and "tellers" to logical variables, bag channels; is
purely declarative
 JoCaml
 Join Java – concurrent language based on the Java programming language
 Joule – dataflow language, communicates by message passing
 Joyce – a concurrent teaching language built on Concurrent Pascal with features from
CSP by Per Brinch Hansen
 LabVIEW – graphical, dataflow programming language, in which functions are nodes in
a graph and data is wires between those nodes. Includes object oriented language
extensions.
 Limbo – relative of Alef, used for systems programming in Inferno ( operating system)
 MultiLisp – Scheme variant extended to support parallelism
 Modula-3 – modern language in Algol family with extensive support for threads,
mutexes, condition variables.
 Newsqueak – research language with channels as first-class values; predecessor of Alef
 occam – influenced heavily by Communicating Sequential Processes ( CSP).
o occam-π – a modern variant of occam, which incorporates ideas from Milner's
π-calculus
 Orc – a heavily concurrent, nondeterministic language based on Kleene algebra.
 Oz – multiparadigm language, supports shared-state and message-passing
concurrency, and futures
o Mozart Programming System – multiplatform Oz
 Pict – essentially an executable implementation of Milner's π-calculus
 Perl with AnyEvent and Coro
 Python with greenlet and gevent.
 Reia – uses asynchronous message passing between shared-nothing objects
 SALSA – actor language with token-passing, join, and first-class continuations for
distributed computing over the Internet
 Scala – a general purpose programming language designed to express common
programming patterns in a concise, elegant, and type-safe way
 SR – research language
 Stackless Python
 SuperPascal – a concurrent teaching language built on Concurrent Pascal and Joyce by
Per Brinch Hansen
 Unicon – Research language.
 Termite Scheme adds Erlang-like concurrency to Scheme
 TNSDL – a language used at developing telecommunication exchanges, uses
asynchronous message passing
 VHDL – VHSIC Hardware Description Language, aka IEEE STD-1076
 XC – a concurrency-extended subset of the C programming language developed by
XMOS based on Communicating Sequential Processes. The language also offers built-in
constructs for programmable I/O.
Many other languages provide support for concurrency in the form of libraries ( on level
roughly comparable with the above list).

### Models of concurrency

There are several models of concurrent computing, which can be used to understand and
analyze concurrent systems. These models include:
 Actor model
o Object-capability model for security
 Petri nets
 Process calculi such as
o Ambient calculus
o Calculus of Communicating Systems ( CCS)
o Communicating Sequential Processes ( CSP)
o π-calculus

### See also

 List of important publications in concurrent, parallel, and distributed computing
 Ptolemy Project
 Race condition
 Critical section
 Transaction processing
 Chu space
 Sheaf ( mathematics)
 Software transactional memory
 Flow-based programming

### References

1. ^ a b Ben-Ari, Mordechai ( 2006). Principles of Concurrent and Distributed Programming
( 2nd ed.). Addison-Wesley. ISBN 978-0-321-31283-9.
2. ^ Armstrong, Joe ( 2003). "Making reliable distributed systems in the presence of
software errors".

### Further reading

 Downey, Allen B. ( 2005) [2005]. The Little Book of Semaphores. Green Tea Press.
ISBN 1441418687.
http://www.greenteapress.com/semaphores/downey08semaphores.pdf.
 Filman, Robert E.; Daniel P. Friedman ( 1984). Coordinated Computing: Tools and
Techniques for Distributed Software. New York: McGraw-Hill. p. 370. ISBN 0-07-
022439-0.
 Leppäjärvi, Jouni ( 2008). A pragmatic, historically oriented survey on the universality of
synchronization primitives. University of Oulu.
http://www.oamk.fi/~joleppaj/personal/jleppaja_gradu_080511.pdf.
 Taubenfeld, Gadi ( 2006). Synchronization Algorithms and Concurrent Programming.
Pearson / Prentice Hall. p. 433. ISBN 0131972596.
http://www.faculty.idc.ac.il/gadi/book.htm.

### External links

 Concurrent Systems Virtual Library
Read more: http://www.answers.com/topic/concurrent-computing#ixzz1FdMjUwW4

## Synchronization

In computer science, synchronization refers to one of two distinct but related concepts:
synchronization of processes, and synchronization of data. Process synchronization
refers to the idea that multiple processes are to join up or handshake at a certain point,
so as to reach an agreement or commit to a certain sequence of action. Data
synchronization refers to the idea of keeping multiple copies of a dataset in coherence
with one another, or to maintain data integrity. Process synchronization primitives are
commonly used to implement data synchronization.
**Contents** [hide]
- 1 Process synchronization
  - 1.1 See
- 2 Data synchronization
- 3 Mathematical foundations
- 4 External links

### Process synchronization

Process synchronization or serialization, strictly defined, is the application of particular
mechanisms to ensure that two concurrently-executing threads or processes do not
execute specific portions of a program at the same time. If one process has begun to
execute a serialized portion of the program, any other process trying to execute this
portion must wait until the first process finishes. Synchronization is used to control
access to state both in small-scale multiprocessing systems -- in multithreaded and
multiprocessor computers -- and in distributed computers consisting of thousands of
units -- in banking and database systems, in web servers, and so on.

#### See

 Lock ( computer science) and Mutex
 Monitor ( synchronization)
 Semaphore ( programming)
 Test-and-set

### Data synchronization

Main article: Data synchronization
A distinctly different ( but related) concept is that of data synchronization. This refers
to the need to keep multiple copies of a set of data coherent with one another.
Examples include:
 File synchronization, such as syncing a hand-held MP3 player to a desktop computer.
 Cluster file systems, which are file systems that maintain data or indexes in a coherent
fashion across a whole computing cluster.
 Cache coherency, maintaining multiple copies of data in sync across multiple caches.
 RAID, where data is written in a redundant fashion across multiple disks, so that the
loss of any one disk does not lead to a loss of data.
 Database replication, where copies of data on a database are kept in sync, despite
possible large geographical separation.
 Journalling, a technique used by many modern file systems to make sure that file
metadata are updated on a disk in a coherent, consistent manner.

### Mathematical foundations

An abstract mathematical foundation for synchronization primitives is given by the
history monoid. There are also many higher-level theoretical devices, such as process
calculi and Petri nets, which can be built on top of the history monoid.

### External links

 Anatomy of Linux synchronization methods at IBM developerWorks
 The Little Book of Semaphores, by Allen B. Downey
Read more: http://www.answers.com/topic/synchronization-computer-
science#ixzz1FdOsOVBF

## Critical section

In concurrent programming a critical section is a piece of code that accesses a shared
resource ( data structure or device) that must not be concurrently accessed by more than
one thread of execution. A critical section will usually terminate in fixed time, and a
thread, task or process will have to wait a fixed time to enter it ( aka bounded waiting).
Some synchronization mechanism is required at the entry and exit of the critical section
to ensure exclusive use, for example a semaphore.
By carefully controlling which variables are modified inside and outside the critical
section ( usually, by accessing important state only from within), concurrent access to
that state is prevented. A critical section is typically used when a multithreaded program
must update multiple related variables without a separate thread making conflicting
changes to that data. In a related situation, a critical section may be used to ensure a
shared resource, for example a printer, can only be accessed by one process at a time.
How critical sections are implemented varies among operating systems.
The simplest method is to prevent any change of processor control inside the critical
section. On uni-processor systems, this can be done by disabling interrupts on entry into
the critical section, avoiding system calls that can cause a context switch while inside
the section and restoring interrupts to their previous state on exit. Any thread of
execution entering any critical section anywhere in the system will, with this
implementation, prevent any other thread, including an interrupt, from getting the CPU
and therefore from entering any other critical section or, indeed, any code whatsoever,
until the original thread leaves its critical section.
This brute-force approach can be improved upon by using semaphores. To enter a
critical section, a thread must obtain a semaphore, which it releases on leaving the
section. Other threads are prevented from entering the critical section at the same time
as the original thread, but are free to gain control of the CPU and execute other code,
including other critical sections that are protected by different semaphores.
Some confusion exists in the literature about the relationship between different critical
sections in the same program.[citation needed] In general, a resource that must be protected
from concurrent access may be accessed by several pieces of code. Each piece must be
guarded by a common semaphore. Is each piece now a critical section or are all the
pieces guarded by the same semaphore in aggregate a single critical section? This
confusion is evident in definitions of a critical section such as "... a piece of code that
can only be executed by one process or thread at a time". This only works if all access
to a protected resource is contained in one "piece of code", which requires either the
definition of a piece of code or the code itself to be somewhat contrived.
**Contents** [hide]
- 1 Application Level Critical Sections
- 2 Kernel Level Critical Sections
- 3 See also
- 4 External links

### Application Level Critical Sections

Application-level critical sections reside in the memory range of the process and are
usually modifiable by the process itself. This is called a user-space object because the
program run by the user ( as opposed to the kernel) can modify and interact with the
object. However the functions called may jump to kernel-space code to register the user-
space object with the kernel.
Example Code For Critical Sections with POSIX pthread library

```

/* Sample C/C++, Unix/Linux */

# include <pthread.h>

/* This is the critical section object ( statically allocated). */
static pthread_mutex_t cs_mutex = PTHREAD_MUTEX_INITIALIZER;
void f ()
{
/* Enter the critical section -- other threads are locked out */
pthread_mutex_lock ( &cs_mutex );
/* Do some thread-safe processing! */
/*Leave the critical section -- other threads can now
pthread_mutex_lock () */
pthread_mutex_unlock ( &cs_mutex );
}

```

Example Code For Critical Sections with Win32 API

```

/* Sample C/C++, Windows, link to kernel32.dll */

# include <windows.h>

static CRITICAL_SECTION cs; /* This is the critical section object --
once initialized,
it cannot be moved in memory */
/* If you program in OOP, declare this as
a non-static member in your class */
/* Initialize the critical section before entering multi-threaded
context. */
InitializeCriticalSection (&cs);
void f ()
{
/* Enter the critical section -- other threads are locked out */
EnterCriticalSection (&cs);
/* Do some thread-safe processing! */
/* Leave the critical section -- other threads can now
EnterCriticalSection () */
LeaveCriticalSection (&cs);
}
/* Release system object when all finished -- usually at the end of
the cleanup code */
DeleteCriticalSection (&cs);

```

Note that on Windows NT ( not 9x/ME), the function TryEnterCriticalSection () can be
used to attempt to enter the critical section. This function returns immediately so that
the thread can do other things if it fails to enter the critical section ( usually due to
another thread having locked it). With the pthreads library, the equivalent function is
pthread_mutex_trylock (). Note that the use of a CriticalSection is not the same as a
Win32 Mutex, which is an object used for inter-process synchronization. A Win32
CriticalSection is for intra-process synchronization ( and is much faster as far as lock
times), however it cannot be shared across processes.

### Kernel Level Critical Sections

This section does not cite any references or sources.
Please help improve this article by adding citations to reliable sources. Unsourced material may
be challenged and removed. ( July 2007)
Typically, critical sections prevent process and thread migration between processors and
the preemption of processes and threads by interrupts and other processes and threads.
Critical sections often allow nesting. Nesting allows multiple critical sections to be
entered and exited at little cost.
If the scheduler interrupts the current process or thread in a critical section, the
scheduler will either allow the process or thread to run to completion of the critical
section, or it will schedule the process or thread for another complete quantum. The
scheduler will not migrate the process or thread to another processor, and it will not
schedule another process or thread to run while the current process or thread is in a
critical section.
Similarly, if an interrupt occurs in a critical section, the interrupt's information is
recorded for future processing, and execution is returned to the process or thread in the
critical section. Once the critical section is exited, and in some cases the scheduled
quantum completes, the pending interrupt will be executed.
Since critical sections may execute only on the processor on which they are entered,
synchronization is only required within the executing processor. This allows critical
sections to be entered and exited at almost zero cost. No interprocessor synchronization
is required, only instruction stream synchronization. Most processors provide the
required amount of synchronization by the simple act of interrupting the current
execution state. This allows critical sections in most cases to be nothing more than a per
processor count of critical sections entered.
Performance enhancements include executing pending interrupts at the exit of all
critical sections and allowing the scheduler to run at the exit of all critical sections.
Furthermore, pending interrupts may be transferred to other processors for execution.
Critical sections should not be used as a long-lived locking primitive. They should be
short enough that the critical section will be entered, executed, and exited without any
interrupts occurring, neither from hardware much less the scheduler.
Kernel Level Critical Sections are the base of the software lockout issue.

### See also

 Lock ( computer science)

### External links

Critical Section documentation on the MSDN Library homepage:
http://msdn2.microsoft.com/en-us/library/ms682530.aspx
Read more: http://www.answers.com/topic/critical-section#ixzz1FdOVsoTZ

## Mutual exclusion

Mutual exclusion ( often abbreviated to mutex) algorithms are used in concurrent
programming to avoid the simultaneous use of a common resource, such as a global
variable, by pieces of computer code called critical sections. A critical section is a piece
of code in which a process or thread accesses a common resource. The critical section
by itself is not a mechanism or algorithm for mutual exclusion. A program, process, or
thread can have the critical section in it without any mechanism or algorithm which
implements mutual exclusion.
Examples of such resources are fine-grained flags, counters or queues, used to
communicate between code that runs concurrently, such as an application and its
interrupt handlers. The synchronization of access to those resources is an acute problem
because a thread can be stopped or started at any time.
To illustrate: suppose a section of code is altering a piece of data over several program
steps, when another thread, perhaps triggered by some unpredictable event, starts
executing. If this second thread reads from the same piece of data, the data, which is in
the process of being overwritten, is in an inconsistent and unpredictable state. If the
second thread tries overwriting that data, the ensuing state will probably be
unrecoverable. These shared data being accessed by critical sections of code, must
therefore be protected, so that other processes which read from or write to the chunk of
data are excluded from running.
A mutex is also a common name for a program object that negotiates mutual exclusion
among threads, also called a lock.
**Contents** [hide]
- 1 Enforcing mutual exclusion
  - 1.1 Hardware solutions
  - 1.2 Software solutions
- 2 Advanced mutual exclusion
- 3 Further reading
- 4 See also
- 5 External links

### Enforcing mutual exclusion

There are both software and hardware solutions for enforcing mutual exclusion. The
different solutions are shown below.

#### Hardware solutions

On a uniprocessor system a common way to achieve mutual exclusion inside kernels is
to disable interrupts for the smallest possible number of instructions that will prevent
corruption of the shared data structure, the critical section. This prevents interrupt code
from running in the critical section, that also protects against interrupt-based process-
change.
In a computer in which several processors share memory, an indivisible test-and-set of a
flag could be used in a tight loop to wait until the other processor clears the flag. The
test-and-set performs both operations without releasing the memory bus to another
processor. When the code leaves the critical section, it clears the flag. This is called a
"spinlock" or "busy-wait".
Similar atomic multiple-operation instructions, e.g., compare-and-swap, are commonly
used for lock-free manipulation of linked lists and other data structures.

#### Software solutions

Beside the hardware supported solution, some software solutions exist that use "busy-
wait" to achieve the goal. Examples of these include the following:
 Dekker's algorithm
 Peterson's algorithm
 Lamport's bakery algorithm
 The black-white bakery algorithm
 Szymanski's Algorithm
Unfortunately, spin locks and busy waiting take up excessive processor time and power
and are considered anti-patterns in almost every case. In addition, these algorithms do
not work if Out-of-order execution is utilized on the platform that executes them.
Programmers have to specify strict ordering on the memory operations within a
thread.[citation needed]
The solution to these problems is to use synchronization facilities provided by an
operating system's multithreading library, which will take advantage of hardware
solutions if possible but will use software solutions if no hardware solutions exist. For
example, when the operating system's lock library is used and a thread tries to acquire
an already acquired lock, the operating system will suspend the thread using a context
switch and swaps it out with another thread that is ready to be run, or could put that
processor into a low power state if there is no other thread that can be run. Therefore,
most modern mutual exclusion methods attempt to reduce latency and busy-waits by
using queuing and context switches. However, if the time that is spent suspending a
thread and then restoring it can be proven to be always more than the time that must be
waited for a thread to become ready to run after being blocked in a particular situation,
then spinlocks are a fine solution for that situation only.

### Advanced mutual exclusion

Synchronization primitives can be built like the examples below by using the solutions
explained above:
 Locks
 Reentrant mutexes
 Semaphores
 Monitors
 Message passing
 Tuple space
Many forms of mutual exclusion have side-effects. For example, classic semaphores
permit deadlocks, in which one process gets a semaphore, another process gets a second
semaphore, and then both wait forever for the other semaphore to be released. Other
common side-effects include starvation, in which a process never gets sufficient
resources to run to completion, priority inversion in which a higher priority thread waits
for a lower-priority thread, and "high latency" in which response to interrupts is not
prompt.
Much research is aimed at eliminating the above effects, such as by guaranteeing non-
blocking progress. No perfect scheme is known.

### Further reading

 Michel Raynal: Algorithms for Mutual Exclusion, MIT Press, ISBN 0-262-
18119-3
 Sunil R. Das, Pradip K. Srimani: Distributed Mutual Exclusion Algorithms,
IEEE Computer Society, ISBN 0-8186-3380-8
 Thomas W. Christopher, George K. Thiruvathukal: High-Performance Java
Platform Computing, Prentice Hall, ISBN 0-13-016164-0
 Gadi Taubenfeld, Synchronization Algorithms and Concurrent Programming,
Pearson/Prentice Hall, ISBN 0-13-197259-6

### See also

 Atomicity ( programming)
 Concurrency control
 Mutually exclusive events
 Semaphore
 Dining philosophers problem
 Reentrant mutex

### External links

 Article "Common threads: POSIX threads explained - The little things called
mutexes" by Daniel Robbins
 Mutual exclusion algorithm discovery
 Mutual Exclusion Petri Net
 Mutual Exclusion with Locks - an Introduction
 Mutual exclusion variants in OpenMP
 The Black-White Bakery Algorithm

## Lock

In computer science, a lock is a synchronization mechanism for enforcing limits on
access to a resource in an environment where there are many threads of execution.
Locks are one way of enforcing concurrency control policies.
Contents [hide]
 1 Types
 2 Granularity
 3 Database locks
 4 The problems with locks
 5 Language support
 6 See also
 7 References

### Types

Generally, locks are advisory locks, where each thread cooperates by acquiring the lock
before accessing the corresponding data. Some systems also implement mandatory
locks, where attempting unauthorized access to a locked resource will force an
exception in the entity attempting to make the access.
A ( binary) semaphore is the simplest type of lock. In terms of access to the data, no
distinction is made between shared ( read only) or exclusive ( read and write) modes.
Other schemes provide for a shared mode, where several threads can acquire a shared
lock for read-only access to the data. Other modes such as exclusive, intend-to-exclude
and intend-to-upgrade are also widely implemented.
Independent of the type of lock chosen above, locks can be classified by what happens
when the lock strategy prevents progress of a thread. Most locking designs block the
execution of the thread requesting the lock until it is allowed to access the locked
resource. A spinlock is a lock where the thread simply waits ("spins") until the lock
becomes available. It is very efficient if threads are only likely to be blocked for a short
period of time, as it avoids the overhead of operating system process re-scheduling. It is
wasteful if the lock is held for a long period of time.
Locks typically require hardware support for efficient implementation. This usually
takes the form of one or more atomic instructions such as "test-and-set", "fetch-and-
add" or "compare-and-swap". These instructions allow a single process to test if the
lock is free, and if free, acquire the lock in a single atomic operation.
Uniprocessor architectures have the option of using uninterruptable sequences of
instructions, using special instructions or instruction prefixes to disable interrupts
temporarily, but this technique does not work for multiprocessor shared-memory
machines. Proper support for locks in a multiprocessor environment can require quite
complex hardware and/or software support, with substantial synchronization issues.
The reason an atomic operation is required is because of concurrency, where more than
one task executes the same logic. For example, consider the following C code:

```

if ( lock == 0) lock = myPID; /* lock free - set it */

```

The above example does not guarantee that the task has the lock, since more than one
task can be testing the lock at the same time. Since both tasks will detect that the lock is
free, both tasks will attempt to set the lock, not knowing that the other task is also
setting the lock. Dekker's or Peterson's algorithm are possible substitutes if atomic
locking operations are not available.
Careless use of locks can result in deadlock or livelock. Deadlock occurs when a
process holds a lock and then attempts to acquire a second lock. If the second lock is
already held by another process, the first process will be blocked. If the second process
then attempts to acquire the lock held by the first process, the system has "deadlocked":
no progress will ever be made. A number of strategies can be used to avoid or recover
from deadlocks, both at design-time and at run-time. ( The most common is to
standardize the lock acquisition sequences so that combinations of inter-dependent
locks are always acquired and released in a specifically defined "cascade" order.)

### Granularity

Before being introduced to lock granularity, one needs to understand three concepts
about locks.
 lock overhead: The extra resources for using locks, like the memory space
allocated for locks, the CPU time to initialize and destroy locks, and the time for
acquiring or releasing locks. The more locks a program uses, the more overhead
associated with the usage.
 lock contention: This occurs whenever one process or thread attempts to
acquire a lock held by another process or thread. The more granular the available
locks, the less likely one process/thread will request a lock held by the other.
( For example, locking a row rather than the entire table, or locking a cell rather
than the entire row.)
 deadlock: The situation when each of two tasks is waiting for a lock that the
other task holds. Unless something is done, the two tasks will wait forever.
So there is a tradeoff between decreasing lock overhead and decreasing lock contention
when choosing the number of locks in synchronization.
An important property of a lock is its granularity. The granularity is a measure of the
amount of data the lock is protecting. In general, choosing a coarse granularity ( a small
number of locks, each protecting a large segment of data) results in less lock overhead
when a single process is accessing the protected data, but worse performance when
multiple processes are running concurrently. This is because of increased lock
contention. The more coarse the lock, the higher the likelihood that the lock will stop
an unrelated process from proceeding. Conversely, using a fine granularity ( a larger
number of locks, each protecting a fairly small amount of data) increases the overhead
of the locks themselves but reduces lock contention. More locks also increase the risk of
deadlock.[citation needed]
In a database management system, for example, a lock could protect, in order of
increasing granularity, part of a field, a field, a record, a data page, or an entire table.
Coarse granularity, such as using table locks, tends to give the best performance for a
single user, whereas fine granularity, such as record locks, tends to give the best
performance for multiple users.

### Database locks

Main article: Lock ( database)
Database locks can be used as a means of ensuring transaction synchronicity. i.e. when
making transaction processing concurrent ( interleaving transactions), using 2-phased
locks ensures that the concurrent execution of the transaction turns out equivalent to
some serial ordering of the transaction. However, deadlocks become an unfortunate
side-effect of locking in databases. Deadlocks are either prevented by pre-determining
the locking order between transactions or are detected using waits-for graphs. An
alternate to locking for database synchronicity while avoiding deadlocks involves the
use of totally ordered global timestamps.
There are mechanisms employed to manage the actions of multiple concurrent users on
a database - the purpose is to prevent lost updates and dirty reads. The two types of
locking are Pessimistic and Optimistic Locking.
 Pessimistic locking: A user who reads a record, with the intention of updating
it, places an exclusive lock on the record to prevent other users from
manipulating it. This means no one else can manipulate that record until the user
releases the lock. The downside is that users can be locked out for a very long
time, thereby slowing the overall system response and causing frustration.
o Where to use pessimistic locking: This is mainly used in environments
where data-contention ( the degree of users request to the database system
at any one time) is heavy; where the cost of protecting data through locks
is less than the cost of rolling back transactions if concurrency conflicts
occur. Pessimistic concurrency is best implemented when lock times will
be short, as in programmatic processing of records. Pessimistic
concurrency requires a persistent connection to the database and is not a
scalable option when users are interacting with data, because records
might be locked for relatively large periods of time. It is not appropriate
for use in web application development.
 Optimistic locking: this allows multiple concurrent users access to the database
whilst the system keeps a copy of the initial-read made by each user. When a
user wants to update a record, the application determines whether another user
has changed the record since it was last read. The application does this by
comparing the initial-read held in memory to the database record to verify any
changes made to the record. Any discrepancies between the initial-read and the
database record violates concurrency rules and hence causes the system to
disregard any update request. An error message is generated and the user is
asked to start the update process again. It improves database performance by
reducing the amount of locking required, thereby reducing the load on the
database server. It works efficiently with tables that require limited updates since
no users are locked out. However, some updates may fail. The downside is
constant update failures due to high volumes of update requests from multiple
concurrent users - it can be frustrating for users.
o Where to use optimistic locking: This is appropriate in environments
where there is low contention for data, or where read-only access to data
is required. Optimistic concurrency is used extensively in .NET to
address the needs of mobile and disconnected applications,[1] where
locking data rows for prolonged periods of time would be infeasible.
Also, maintaining record locks requires a persistent connection to the
database server, which is not possible in disconnected applications.

### The problems with locks

Lock-based resource protection and thread/process synchronization have many
disadvantages:
 They cause blocking, which means some threads/processes have to wait until a
lock ( or a whole set of locks) is released.
 Lock handling adds overhead for each access to a resource, even when the
chances for collision are very rare. ( However, any chance for such collisions is a
race condition.)
 Locks can be vulnerable to failures and faults that are often very subtle and may
be difficult to reproduce reliably. One example is the deadlock. If one thread
holding a lock dies, stalls/blocks or goes into any sort of infinite loop, other
threads waiting for the lock may wait forever.
 Lock contention limits scalability and adds complexity.
 Balances between lock overhead and contention can be unique to given problem
domains ( applications) as well as sensitive to design, implementation, and even
low-level system architectural changes. These balances may change over the life
cycle of any given application/implementation and may entail tremendous
changes to update ( re-balance).
 Locks are only composable ( e.g., managing multiple concurrent locks in order to
atomically delete Item X from Table A and insert X into Table B) with relatively
elaborate ( overhead) software support and perfect adherence by applications
programming to rigorous conventions.
 Priority inversion. High priority threads/processes cannot proceed if a low
priority thread/process is holding the common lock.
 Convoying. All other threads have to wait if a thread holding a lock is
descheduled due to a time-slice interrupt or page fault ( See lock convoy)
 Hard to debug: Bugs associated with locks are time dependent. They are
extremely hard to replicate.
 There must be sufficient resources - exclusively dedicated memory, real or
virtual - available for the locking mechanisms to maintain their state information
in response to a varying number of contemporaneous invocations, without which
the mechanisms will fail, or "crash" bringing down everything depending on
them and bringing down the operating region in which they reside. "Failure" is
better than crashing, which means a proper locking mechanism ought to be able
to return an "unable to obtain lock for `<whatever>` reason" status to the critical
section in the application, which ought to be able to handle that situation
gracefully. The logical design of an application requires these considerations
from the very root of conception.
Some people use a concurrency control strategy that doesn't have some or all of these
problems. For example, some people use a funnel or serializing tokens, which makes
their software immune to the biggest problem -- deadlocks. Other people avoid locks
entirely -- using non-blocking synchronization methods, like lock-free programming
techniques and transactional memory. However, many of the above disadvantages have
analogues with these alternative synchronization methods.

### Language support

See also: Barrier ( computer science)
Language support for locking depends on the language used:
 There is no API to handle mutexes in the ISO/IEC standards for C or C++. The
upcoming revision of the ISO C++ standard, informally known as C++0x, will
support threading facilities. The OpenMP standard is supported by some
compilers, and this provides critical sections to be specified using pragmas. The
POSIX pthread API provides lock support, but its use is not straightforward.[2]
Visual C++ allows adding the synchronize attribute in the code to mark methods
that must be synchronized, but this is specific to "COM objects" in the Windows
architecture and Visual C++ compiler.[3] C and C++ can easily access any native
operating system locking features.
 Java provides the keyword synchronized to put locks on blocks of code, methods
or objects[4] and libraries featuring concurrency-safe data structures.
 In the C# programming language, the lock keyword can be used to ensure that a
thread has exclusive access to a certain resource.
 VB.NET provides a SyncLock keyword for the same purpose of C#'s lock
keyword.
 Python does not provide a lock keyword, but it is possible to use a lower level
mutex mechanism to acquire or release a lock.[5]
 Ruby also doesn't provide a keyword for synchronization, but it is possible to
use an explicit low level mutex object.[6]
 In x86 Assembly, the LOCK prefix prevents another processor from doing
anything in the middle of certain operations: it guarantees atomicity.
 Objective-C provides the keyword "@synchronized"[7] to put locks on blocks of
code and also provides the classes NSLock[8], NSRecursiveLock[9], and
NSConditionLock[10] along with the NSLocking protocol[11] for locking as well.
 Ada is probably worth looking at too for a comprehensive overview, with its
protected objects[12][13] and rendez-vouses.

### See also

 Mutex
 Semaphore ( programming)
 Monitor ( synchronization)
 Mutual exclusion
 Critical section
 Lock-free and wait-free algorithms
 File locking
 Read/write lock pattern
 Double-checked locking

### References

1. ^ "Designing Data Tier Components and Passing Data Through Tiers".
Microsoft. August 2002. http://msdn.microsoft.com/en-
us/library/ms978496.aspx. Retrieved 2008-05-30.
2. ^ Marshall, Dave ( March 1999). "Mutual Exclusion Locks".
http://www.cs.cf.ac.uk/Dave/C/node31.html#SECTION00311000000000000000
0. Retrieved 2008-05-30.
3. ^ "Synchronize". msdn.microsoft.com. http://msdn.microsoft.com/en-
us/library/34d2s8k3 ( VS.80).aspx. Retrieved 2008-05-30.
4. ^ "Synchronization". Sun Microsystems.
http://java.sun.com/docs/books/tutorial/essential/concurrency/sync.html.
Retrieved 2008-05-30.
5. ^ Lundh, Fredrik ( July 2007). "Thread Synchronization Mechanisms in Python".
http://effbot.org/zone/thread-synchronization.htm. Retrieved 2008-05-30.
6. ^ "Programming Ruby: Threads and Processes". 2001. http://www.ruby-
doc.org/docs/ProgrammingRuby/html/tut_threads.html. Retrieved 2008-05-30.
7. ^ "Apple Threading Reference". Apple, inc.
http://developer.apple.com/mac/library/documentation/Cocoa/Conceptual/Objec
tiveC/Articles/ocThreading.html. Retrieved 2009-10-17.
8. ^ "NSLock Reference". Apple, inc.
http://developer.apple.com/mac/library/documentation/Cocoa/Reference/Founda
tion/Classes/NSLock_Class/Reference/Reference.html. Retrieved 2009-10-17.
9. ^ "NSRecursiveLock Reference". Apple, inc.
http://developer.apple.com/mac/library/documentation/Cocoa/Reference/Founda
tion/Classes/NSRecursiveLock_Class/Reference/Reference.html. Retrieved
2009-10-17.
10. ^ "NSConditionLock Reference". Apple, inc.
http://developer.apple.com/mac/library/documentation/Cocoa/Reference/Founda
tion/Classes/NSConditionLock_Class/Reference/Reference.html. Retrieved
2009-10-17.
11. ^ "NSLocking Protocol Reference". Apple, inc.
http://developer.apple.com/mac/library/documentation/Cocoa/Reference/Founda
tion/Protocols/NSLocking_Protocol/Reference/Reference.html. Retrieved 2009-
10-17.
12. ^ ISO/IEC 8652:2007. "Protected Units and Protected Objects". Ada 2005
Reference Manual. http://www.adaic.com/standards/1zrm/html/RM-9-4.html.
Retrieved 2010-02-37. "A protected object provides coordinated access to
shared data, through calls on its visible protected operations, which can be
protected subprograms or protected entries."
13. ^ ISO/IEC 8652:2007. "Example of Tasking and Synchronization". Ada 2005
Reference Manual. http://www.adaic.com/standards/1zrm/html/RM-9-11.html.
Retrieved 2010-02-37.

## Monitor

In concurrent programming, a monitor is an object or module intended to be used
safely by more than one thread. The defining characteristic of a monitor is that its
methods are executed with mutual exclusion. That is, at each point in time, at most one
thread may be executing any of its methods. This mutual exclusion greatly simplifies
reasoning about the implementation of monitors compared with code that may be
executed in parallel.
Monitors also provide a mechanism for threads to temporarily give up exclusive access,
in order to wait for some condition to be met, before regaining exclusive access and
resuming their task. Monitors also have a mechanism for signaling other threads that
such conditions have been met.
Monitors were invented by C. A. R. Hoare [1] and Per Brinch Hansen, [2] and were first
implemented in Brinch Hansen's Concurrent Pascal language.
Contents
 1 Mutual exclusion
 2 Waiting and signaling
o 2.1 Blocking condition variables
o 2.2 Nonblocking condition variables
o 2.3 Implicit condition variable monitors
o 2.4 Implicit signaling
 3 History
 4 See also
 5 Bibliography
 6 External links
 7 Notes

### Mutual exclusion

As a simple example, consider a monitor for performing transactions on a bank account.

```

monitor class Account {
private int balance := 0
invariant balance >= 0
public method boolean withdraw ( int amount)
precondition amount >= 0
{
if balance < amount then return false
else { balance := balance - amount ; return true }
}
public method deposit ( int amount)
precondition amount >= 0
{
balance := balance + amount
}
}

```

While a thread is executing a method of a monitor, it is said to occupy the monitor.
Monitors are implemented to enforce that at each point in time, at most one thread may
occupy the monitor. This is the monitor's mutual exclusion property.
Upon calling one of the methods, a thread must wait until no other thread is executing
any of the monitor's methods before starting execution of its method. Note that without
this mutual exclusion, in the present example, two threads could cause money to be lost
or gained for no reason. For example two threads withdrawing 1000 from the account
could both return true, while causing the balance to drop by only 1000, as follows: first,
both threads fetch the current balance, find it greater than 1000, and subtract 1000 from
it; then, both threads store the balance and return.
In a simple implementation, mutual exclusion can be implemented by the compiler
equipping each monitor object with a private lock, often in the form of a semaphore.
This lock, which is initially unlocked, is locked at the start of each public method, and is
unlocked at each return from each public method.

### Waiting and signaling

For many applications, mutual exclusion is not enough. Threads attempting an operation
may need to wait until some condition P holds true. A busy waiting loop

```

while not ( P ) do skip

```

will not work, as mutual exclusion will prevent any other thread from entering the
monitor to make the condition true.
The solution is condition variables. Conceptually a condition variable is a queue of
threads, associated with a monitor, on which a thread may wait for some condition to
become true. Thus each condition variable c is associated with an assertion P . While a
c
thread is waiting on a condition variable, that thread is not considered to occupy the
monitor, and so other threads may enter the monitor to change the monitor's state. In
most types of monitors, these other threads may signal the condition variable c to
indicate that assertion P is true in the current state.
c
Thus there are two main operations on condition variables:
 wait c is called by a thread that needs to wait until the assertion P is true
c
before proceeding. While the thread is waiting, it does not occupy the monitor.
 signal c ( sometimes written as notify c) is called by a thread to indicate that
the assertion P is true.
c
As an example, consider a monitor that implements a semaphore. There are methods to
increment ( V) and to decrement ( P) a private integer s. However, the integer must never
be decremented below 0; thus a thread that tries to decrement must wait until the integer
is positive. We use a condition variable sIsPositive with an associated assertion of
P = ( s > 0).
sIsPositive

```

monitor class Semaphore
{
private int s := 0
invariant s >= 0
private Condition sIsPositive /* associated with s > 0 */
public method P ()
{
if s = 0 then wait sIsPositive
assert s > 0
s := s - 1
}
public method V ()
{
s := s + 1
assert s > 0
signal sIsPositive
}
}

```

When a signal happens on a condition variable that at least one other thread is waiting
on, there are at least two threads that could then occupy the monitor: the thread that
signals and any one of the threads that is waiting. In order that at most one thread
occupies the monitor at each time, a choice must be made. Two schools of thought exist
on how best to resolve this choice. This leads to two kinds of condition variables which
will be examined next:
 Blocking condition variables or Signal and Wait give priority to a signaled
thread.
 Nonblocking condition variables or Signal and Continue give priority to the
signaling thread.

#### Blocking condition variables

The original proposals by C. A. R. Hoare and Per Brinch Hansen were for blocking
condition variables. Monitors using blocking condition variables are often called Hoare
style monitors. With a blocking condition variable, the signaling thread must wait
outside the monitor ( at least) until the signaled thread relinquishes occupancy of the
monitor by either returning or by again waiting on a condition variable.
*[Diagrama de Wikipedia no recuperado en la extracción: ilustraba un monitor de estilo Hoare con dos variables de condición, "a" y "b" (atribuido a Buhr et al.).]*
We assume there are two queues of threads associated with each monitor object
 e is the entrance queue
 s is a queue of threads that have signaled.
In addition we assume that for each condition variable c, there is a queue
 c.q, which is a queue for threads waiting on condition variable c
All queues are typically guaranteed to be fair ( in all futures, each thread that enters the
queue will be chosen infinitely often citation needed) and, in some implementations,
may be guaranteed to be first in first out.
The implementation of each operation is as follows. ( We assume that each operation
runs in mutual exclusion to the others; thus restarted threads do not begin executing
until the operation is complete.)

```

enter the monitor:
enter the method
if the monitor is locked
add this thread to e
block this thread
else
lock the monitor
leave the monitor:
schedule
return from the method
wait c :
add this thread to c.q
schedule
block this thread
signal c :
if there is a thread waiting on c.q
select and remove one such thread t from c.q
( t is called "the signaled thread")
add this thread to s
restart t
( so t will occupy the monitor next)
block this thread
schedule :
if there is a thread on s
select and remove one thread from s and restart it
( this thread will occupy the monitor next)
else if there is a thread on e
select and remove one thread from e and restart it
( this thread will occupy the monitor next)
else
unlock the monitor
( the monitor will become unoccupied)

```

The schedule routine selects the next thread to occupy the monitor or, in the absence of
any candidate threads, unlocks the monitor.
The resulting signaling discipline is known a "signal and urgent wait," as the signaler
must wait, but is given priority over threads on the entrance queue. An alternative is
"signal and wait," in which there is no s queue and signaler waits on the e queue
instead.
Some implementations provide a signal and return operation that combines signaling
with returning from a procedure.

```

signal c and return :
if there is a thread waiting on c.q
select and remove one such thread t from c.q
( t is called "the signaled thread")
restart t
( so t will occupy the monitor next)
else
schedule
return from the method

```

In either case ("signal and urgent wait" or "signal and wait"), when a condition variable
is signaled and there is at least one thread on waiting on the condition variable, the
signaling thread hands occupancy over to the signaled thread seamlessly, so that no
other thread can gain occupancy in between. If P is true at the start of each signal c
c
operation, it will be true at the end of each wait c operation. This is summarized by the
following contracts. In these contracts, I is the monitor's invariant.

```

enter the monitor:
postcondition I
leave the monitor:
precondition I
wait c :
precondition I
modifies the state of the monitor
postcondition P and I
c
signal c :
precondition P and I
c
modifies the state of the monitor
postcondition I
signal c and return :
precondition P and I
c

```

In these contracts, it is assumed that I and P do not depend on the contents or lengths of
c
any queues.
( When the condition variable can be queried as to the number of threads waiting on its
queue, more sophisticated contracts can be given. For example, a useful pair of
contracts, allowing occupancy to be passed without establishing the invariant, is

```

wait c :
precondition I
modifies the state of the monitor
postcondition P
c
signal c
precondition ( not empty ( c) and P ) or ( empty ( c) and I)
c
modifies the state of the monitor
postcondition I

```

See Howard[3] and Buhr et al.,[4] for more).
It is important to note here that the assertion P is entirely up to the programmer; he or
c
she simply needs to be consistent about what it is.
We conclude this section with an example of a blocking monitor that implements a
bounded, thread safe stack.

```

monitor class SharedStack {
private const capacity := 10
private int[capacity] A
private int size := 0
invariant 0 <= size and size <= capacity
private BlockingCondition theStackIsNotEmpty /* associated with 0 <
size and size <= capacity */
private BlockingCondition theStackIsNotFull /* associated with 0 <=
size and size < capacity */
public method push ( int value)
{
if size = capacity then wait theStackIsNotFull
assert 0 <= size and size < capacity
A[size] := value ; size := size + 1
assert 0 < size and size <= capacity
signal theStackIsNotEmpty and return
}
public method int pop ()
{
if size = 0 then wait theStackIsNotEmpty
assert 0 < size and size <= capacity
size := size - 1 ;
assert 0 <= size and size < capacity
signal theStackIsNotFull and return A[size]
}
}

```

#### Nonblocking condition variables

With nonblocking condition variables ( also called "Mesa style" condition variables or
"signal and continue" condition variables), signaling does not cause the signaling thread
to lose occupancy of the monitor. Instead the signaled threads are moved to the e queue.
There is no need for the s queue.
*[Diagrama de Wikipedia no recuperado en la extracción: ilustraba un monitor de estilo Mesa con dos variables de condición, "a" y "b".]*
With nonblocking condition variables, the signal operation is often called notify — a
terminology we will follow here. It is also common to provide a notify all operation
that moves all threads waiting on a condition variable to the e queue.
The meaning of various operations are given here. ( We assume that each operation runs
in mutual exclusion to the others; thus restarted threads do not begin executing until the
operation is complete.)

```

enter the monitor:
enter the method
if the monitor is locked
add this thread to e
block this thread
else
lock the monitor
leave the monitor:
schedule
return from the method
wait c :
add this thread to c.q
schedule
block this thread
notify c :
if there is a thread waiting on c.q
select and remove one thread t from c.q
( t is called "the notified thread")
move t to e
notify all c :
move all threads waiting on c.q to e
schedule :
if there is a thread on e
select and remove one thread from e and restart it
else
unlock the monitor

```

As a variation on this scheme, the notified thread may by moved to a queue called w,
which has priority over e. See Howard[5] and Buhr et al.[6] for further discussion.
It is possible to associate an assertion P with each condition variable c such that P is
c c
sure to be true upon return from wait c. However, one must ensure that P is preserved
c
from the time the notifying thread gives up occupancy until the notified thread is
selected to re-enter the monitor. Between these times there could be activity by other
occupants. Thus it is common for P to simply be true.
c
For this reason, it is usually necessary to enclose each wait operation in a loop like this

```

while not ( P ) do wait c

```

where P is some condition stronger than P . The operations notify c and notify all
c
c are treated as "hints" that P may be true for some waiting thread. Every iteration of
such a loop past the first represents a lost notification; thus with nonblocking monitors,
one must be careful to ensure that too many notifications can not be lost.
As an example of "hinting" consider a bank account in which a withdrawing thread will
wait until the account has sufficient funds before proceeding

```

monitor class Account {
private int balance := 0
invariant balance >= 0
private NonblockingCondition balanceMayBeBigEnough
public method withdraw ( int amount)
precondition amount >= 0
{
while balance < amount do wait balanceMayBeBigEnough
assert balance >= amount
balance := balance - amount
}
public method deposit ( int amount)
precondition amount >= 0
{
balance := balance + amount
notify all balanceMayBeBigEnough
}
}

```

In this example, the condition being waited for is a function of the amount to be
withdrawn, so it is impossible for a depositing thread to know that it made such a
condition true. It makes sense in this case to allow each waiting thread into the monitor
( one at a time) to check if its assertion is true.

#### Implicit condition variable monitors

*[Diagrama de Wikipedia no recuperado en la extracción: ilustraba un monitor de estilo Java.]*
In the Java language, each object may be used as a monitor. ( However, methods that
require mutual exclusion must be explicitly marked as synchronized.) Rather than
having explicit condition variables, each monitor ( i.e. object) is equipped with a single
wait queue, in addition to its entrance queue. All waiting is done on this single wait
queue and all notify and notify all operations apply to this queue.
This approach has also been adopted in other languages such as C#.

#### Implicit signaling

Another approach to signaling is to omit the signal operation. Whenever a thread leaves
the monitor ( by returning or waiting) the assertions of all waiting threads are evaluated
until one is found to be true. In such a system, condition variables are not needed, but
the assertions must be explicitly coded. The contract for wait is

```

wait P:
precondition I
modifies the state of the monitor
postcondition P and I

```

### History

C. A. R. Hoare and Per Brinch Hansen developed the idea of monitors around 1972,
based on earlier ideas of their own and of E. W. Dijkstra. [7] Brinch Hansen was the first
to implement monitors. Hoare developed the theoretical framework and demonstrated
their equivalence to semaphores.
Monitors were soon used to structure inter-process communication in the Solo operating
system.
Programming languages that have supported monitors include
 Ada since Ada 95 ( as protected objects)
 C# ( and other languages that use the .NET Framework)
 Concurrent Euclid
 Concurrent Pascal
 D
 Delphi ( Delphi 2009 and above, via TObject.Monitor)
 Java ( via the wait and notify keyword)
 Mesa
 Modula-3
 Python ( via threading.Condition object)
 Ruby
 Squeak Smalltalk
 Turing, Turing+, and Object-Oriented Turing
 μC++
A number of libraries have been written that allow monitors to be constructed in
languages that do not support them natively. When library calls are used, it is up to the
programmer to explicitly mark the start and end of code executed with mutual
exclusion. PThreads is one such library.

### See also

 Mutual exclusion
 Communicating sequential processes - a later development of monitors by C. A.
R. Hoare
 Semaphore ( programming)

### Bibliography

 Monitors: an operating system structuring concept, C. A. R. Hoare -
Communications of the ACM, v.17 n.10, p. 549-557, Oct. 1974 [5]
 Monitor classification P.A. Buhr, M. Fortier, M.H. Coffin - ACM Computing
Surveys, 1995 [6]

### External links

 Java Monitors ( lucid explanation)
 "Monitors: An Operating System Structuring Concept" by C. A. R. Hoare
 "Signalling in Monitors" by John H. Howard ( computer scientist)
 "Proving Monitors" by John H. Howard ( computer scientist)
 "Experience with Processes and Monitors in Mesa" by Butler W. Lampson and
David D. Redell
 pthread_cond_wait - description from the Open Group Base Specifications Issue
6, IEEE Std 1003.1
 "Block on a Condition Variable" by Dave Marshall ( computer scientist)
 "Strategies for Implementing POSIX Condition Variables on Win32" by
Douglas C. Schmidt and Irfan Pyarali
 Condition Variable Routines from the Apache Portable Runtime Library
 wxCondition description
 Boost Condition Variables Reference
 ZThread Condition Class Reference
 Wefts::Condition Class Reference
 ACE_Condition Class Template Reference
 QWaitCondition Class Reference
 Common C++ Conditional Class Reference
 at::ConditionalMutex Class Reference
 threads::shared - Perl extension for sharing data structures between threads
 Tutorial multiprocessing traps
 http://msdn.microsoft.com/en-us/library/ms682052 ( VS.85).aspx
 Monitors in Visual Prolog.

### Notes

1. ^ Hoare, C. A. R. ( 1974), "Monitors: an operating system structuring concept".
Comm. A.C.M. 17 ( 10), 549–57. [1]
2. ^ Brinch Hansen, P. ( 1975). "The programming language Concurrent Pascal".
IEEE Trans. Softw. Eng. 2 ( June), 199–206.
3. ^ John Howard ( 1976), "Signaling in monitors". Proceedings of the 2nd
International Conference on Software Engineering, 47–52
4. ^ Buhr, P.H; Fortier, M., Coffin, M.H. ( 1995). "Monitor classification". ACM
Computing Surveys ( CSUR) 27 ( 1). 63–107. [2]
5. ^ John Howard ( 1976), "Signaling in monitors". Proceedings of the 2nd
International Conference on Software Engineering, 47–52
6. ^ Buhr, P.H; Fortier, M., Coffin, M.H. ( 1995). "Monitor classification". ACM
Computing Surveys ( CSUR) 27 ( 1). 63–107. [3]
7. ^ Brinch Hansen, P. ( 1993). "Monitors and concurrent Pascal: a personal
history", The second ACM SIGPLAN conference on History of programming
languages 1–35. Also published in ACM SIGPLAN Notices 28 ( 3), March 1993.
[4]
This entry is from Wikipedia, the leading user-contributed encyclopedia. It may not
have been reviewed by professional editors ( see full disclaimer)

## Semaphore

In computer science, a semaphore is a protected variable or abstract data type that
provides a simple but useful abstraction for controlling access by multiple processes to a
common resource in a parallel programming environment.
A useful way to think of a semaphore is as a record of how many units of a particular
resource are available, coupled with operations to safely ( i.e. without race conditions)
adjust that record as units are required or become free, and if necessary wait until a unit
of the resource becomes available. Semaphores are a useful tool in the prevention of
race conditions and deadlocks; however, their use is by no means a guarantee that a
program is free from these problems. Semaphores which allow an arbitrary resource
count are called counting semaphores, whilst semaphores which are restricted to the
values 0 and 1 ( or locked/unlocked, unavailable/available) are called binary
semaphores.
The semaphore concept was invented by Dutch computer scientist Edsger Dijkstra,[1]
and the concept has found widespread use in a variety of operating systems.
Contents
- 1 Library analogy
  - 1.1 Important observations
- 2 Semantics and Implementation
- 3 Example: Producer/Consumer Problem
- 4 Function name etymology
- 5 Semaphore vs. mutex
- 6 Current usage
- 7 See also
- 8 Notes and references
- 9 External links

### Library analogy

Suppose a library has 10 identical study rooms, intended to be used by one student at a
time. To prevent disputes, students must request a room from the front counter if they
wish to make use of a study room. When a student has finished using a room, the
student must return to the counter and indicate that one room has become free. If no
rooms are free, students wait at the counter until someone relinquishes a room.
Since the rooms are identical, the librarian at the front desk does not keep track of
which room is occupied, only the number of free rooms available. When a student
requests a room, the librarian decreases this number. When a student releases a room,
the librarian increases this number. Once access to a room is granted, the room can be
used for as long as desired, and so it is not possible to book rooms ahead of time.
In this scenario the front desk represents a semaphore, the rooms are the resources, and
the students represent processes. The value of the semaphore is initially 10. When a
student requests a room he is granted access and the value of the semaphore is changed
to 9. After the next student comes, it drops to 8, then 7 and so on. If someone requests a
room when it is 0, they are forced to wait. When multiple people are waiting, they will
either wait in a queue, or will mill around and race back to the counter when someone
releases a room ( depending on the nature of the semaphore).

#### Important observations

When used for a pool of resources, a semaphore does not keep track of which of the
resources are free, only how many there are. Some other mechanism ( possibly involving
more semaphores) may be required to select a particular free resource.
Processes are trusted to follow the protocol. Fairness and safety are likely to be
compromised ( which practically means a program may behave slowly, act erratically,
hang or crash) if even a single process acts incorrectly. This includes:
 requesting a resource and forgetting to release it,
 releasing a resource that was never requested,
 holding a resource for a long time without needing it, or
 using a resource without requesting it first.
Even if all processes follow these rules, multi-resource deadlock may still occur when
there are different resources managed by different semaphores and when processes need
to use more than one resource at a time, as illustrated by the dining philosophers
problem.

### Semantics and Implementation

Counting semaphores are equipped with two operations, historically denoted as V ( also
known as signal ()) and P ( or wait ())( see below). Operation V increments the semaphore
S, and operation P decrements it. The semantics of these operations is shown below.
Square brackets are used to indicate atomic operations, i.e. operations which appear
indivisible from the perspective of other processes.

```

function V ( semaphore S):
Atomically increment S
[S ← S + 1]
function P ( semaphore S):
repeat:
Between repetitions of the loop other processes may operate on
the semaphore
[if S > 0:
Atomically decrement S - note that S cannot become
negative
S ← S - 1
break]

```

The value of the semaphore S is the number of units of the resource that are currently
available. The P operation wastes time or sleeps until a resource protected by the
semaphore becomes available, at which time the resource is immediately claimed. The
V operation is the inverse: it makes a resource available again after the process has
finished using it.
Many operating systems provide efficient semaphore primitives which mean that one
waiting process is awoken when the semaphore is free. This means that processes do not
waste time checking the semaphore value and context switching unnecessarily.
The counting semaphore concept can be extended with the ability to claim or return
more than one "unit" from the semaphore. a technique implemented in UNIX. The
modified V and P operations are as follows:

```

function V ( semaphore S, integer I):
[S ← S + I]
function P ( semaphore S, integer I):
repeat:
[if S >= I:
S ← S - I
break]

```

To avoid starvation, a semaphore have an associated queue of processes ( usually a first-
in, first out). If a process performs a P operation on a semaphore that has the value zero,
the process is added to the semaphore's queue. When another process increments the
semaphore by performing a V operation, and there are processes on the queue, one of
them is removed from the queue and resumes execution. When processes have different
priorities the queue may be ordered by priority, so that the highest priority process is
taken from the queue first.
If the implementation does not ensure atomicity of the increment, decrement and
comparison operations, then there is a risk of increments or decrements being forgotten,
or of the semaphore value becoming negative. Atomicity may be achieved by using a
machine instruction that is able to read, modify and write the semaphore in a single
operation. In the absence of such a hardware instruction, an atomic operation may be
synthesized through the use of a software mutual exclusion algorithm. On uniprocessor
systems, atomic operations can be ensured by temporarily suspending preemption or
disabling hardware interrupts. This approach does not work on multiprocessor systems
where it is possible for two programs sharing a semaphore to run on different processors
at the same time.

### Example: Producer/Consumer Problem

In the Producer-consumer problem, one process ( the producer) generates data items and
another process ( the consumer) receives and uses them. They communicate using a
queue of maximum size N. Obviously the consumer has to wait for the producer to
produce something if the queue is empty. Perhaps more subtly, the producer has to wait
for the consumer to consume something if the buffer is full.
The problem is easily solved if we model the queue as a series of boxes which are either
empty or full, and regard empty boxes as one type of resource and full boxes as another
type of resource. The producer "removes" an empty box and then "creates" a full one,
whilst the consumer does the reverse.
Given that emptyCount and fullCount are counting semaphores, and emptyCount is
initially N whilst fullCount is initially 0, the producer does the following repeatedly:

```

produce:
P ( emptyCount)
putItemIntoQueue ( item)
V ( fullCount)

```

The consumer does the following repeatedly:-

```

consume:
P ( fullCount)
item ← getItemFromQueue ()
V ( emptyCount)

```

It is important to note that the order of operations is important. For example, if the
producer places the item in the queue after incrementing fullCount, the consumer may
obtain the item before it has been written. If the producer places the item in the queue
before decrementing emptyCount, the producer might exceed the size limit of the queue.

### Function name etymology

The canonical names P and V come from the initials of Dutch words. V stands for
verhogen ("increase"). Several explanations have been offered for P, including proberen
for "to test,"[2] passeer for "pass," probeer for "try," and pakken for "grab." However,
Dijkstra wrote that he intended P to stand for the portmanteau prolaag,[3] short for
probeer te verlagen, literally "try to reduce," or to parallel the terms used in the other
case, "try to decrease."[4][5][6] This confusion stems from the fact that the words for
increase and decrease both begin with the letter V in Dutch, and the words spelled out
in full would be impossibly confusing for those not familiar with the Dutch language.
In ALGOL 68, the Linux kernel,[7] and in some English textbooks, the P and V
operations are called, respectively, down and up. In software engineering practice, they
are often called wait and signal, acquire and release ( which the standard Java library
uses[8]), or pend and post. Some texts call them procure and vacate to match the
original Dutch initials.

### Semaphore vs. mutex

A mutex is essentially the same thing as a binary semaphore, and sometimes uses the
same basic implementation. However, the term "mutex" is used to describe a construct
which prevents two processes from executing the same piece of code, or accessing the
same data, at the same time[citation needed]. The term "binary semaphore" is used to
describe a construct which limits access to a single resource.
In many cases a mutex has a concept of an "owner": the process which locked the mutex
is the only process allowed to unlock it. In contrast, semaphores generally do not have
this restriction, something the producer-consumer example above depends upon.

### Current usage

This section does not cite any references or sources.
Please help improve this article by adding citations to reliable sources. Unsourced material may
be challenged and removed. ( December 2010)
Semaphores are provided by many operating systems as a synchronization primitive,
and are used in many places. However, the trend in programming language development
is towards more structured forms of synchronization, such as monitors. These
synchronization abstractions usually employ semaphores or mutexes internally, but do
not expose the semaphore interface directly to the programmer. This is motivated partly
by the serious, hard-to-diagnose problems that often arise when semaphores are used
incorrectly, a risk much reduced when synchronization is tightly coupled to the resource
it controls and is managed automatically by the language implementation rather than
manually by the programmer.

### See also

 Cigarette smokers problem
 Dining philosophers problem
 Readers-writers problem
 Sleeping barber problem
 Producers-consumers problem
 Reentrant mutex, which can "count" but in a different manner to a counting
semaphore.

### Notes and references

1. ^ http://www.cs.utexas.edu/users/EWD/transcriptions/EWD01xx/EWD123.html
E. W. Dijkstra, Cooperating sequential processes. Technological University,
Eindhoven, The Netherlands, September 1965.
2. ^ Silberschatz, Galvin & Gagne 2008, p. 234
3. ^ http://www.cs.utexas.edu/users/EWD/ewd00xx/EWD74.PDF
4. ^ http://www.cs.utexas.edu/users/EWD/transcriptions/EWD00xx/EWD51.html
MULTIPROGAMMERING EN DE X8 from the E.W. Dijkstra Archive ( in
Dutch)
5. ^ Dijkstra's own translation reads "try-and-decrease", although that phrase might
be confusing for those unaware of the colloquial "try-and..."
6. ^ http://lkml.org/lkml/2005/12/19/34 Linux Kernel Mailing List: [PATCH 1/19]
MUTEX: Introduce simple mutex implementation
7. ^ Kernel hacking howto on linuxgrill.com
8. ^ java.util.concurrent.Semaphore
 Silberschatz, Abraham; Galvin, Peter Baer; Gagne, Greg ( 2008), Operating
System Concepts ( 8th ed.), John Wiley & Sons. Inc, ISBN 978-0-470-12872-5

## Message passing

Message passing in computer science is a form of communication used in parallel
computing, object-oriented programming, and interprocess communication. In this
model, processes or objects can send and receive messages ( comprising zero or more
bytes, complex data structures, or even segments of code) to other processes. By
waiting for messages, processes can also synchronize.
Contents
- 1 Overview
- 2 Message passing systems and models
- 3 Synchronous versus asynchronous message passing
- 4 Message passing versus calling
- 5 Message passing and locks
- 6 Examples of message passing style
- 7 Influences on other programming models
- 8 See also
- 9 References
- 10 External links
- 11 Further reading

### Overview

Message passing is the paradigm of communication where messages are sent from a
sender to one or more recipients. Forms of messages include ( remote) method
invocation, signals, and data packets. When designing a message passing system several
choices are made:
 Whether messages are transferred reliably
 Whether messages are guaranteed to be delivered in order
 Whether messages are passed one-to-one, one-to-many ( multicasting or
broadcasting), or many-to-one ( client–server).
 Whether communication is synchronous or asynchronous.
Prominent theoretical foundations of concurrent computation, such as the Actor model
and the process calculi are based on message passing. Implementations of concurrent
systems that use message passing can either have message passing as an integral part of
the language, or as a series of library calls from the language. Examples of the former
include many distributed object systems. Examples of the latter include Microkernel
operating systems pass messages between one kernel and one or more server blocks,
and the Message Passing Interface used in high-performance computing.

### Message passing systems and models

Distributed object and remote method invocation systems like ONC RPC, Corba, Java
RMI, DCOM, SOAP, .NET Remoting, CTOS, QNX Neutrino RTOS, OpenBinder, D-
Bus and similar are message passing systems.
Message passing systems have been called "shared nothing" systems because the
message passing abstraction hides underlying state changes that may be used in the
implementation of sending messages.
Message passing model based programming languages typically define messaging as
the ( usually asynchronous) sending ( usually by copy) of a data item to a communication
endpoint ( Actor, process, thread, socket, etc.). Such messaging is used in Web Services
by SOAP. This concept is the higher-level version of a datagram except that messages
can be larger than a packet and can optionally be made reliable, durable, secure, and/or
transacted.
Messages are also commonly used in the same sense as a means of interprocess
communication; the other common technique being streams or pipes, in which data are
sent as a sequence of elementary data items instead ( the higher-level version of a virtual
circuit).

### Synchronous versus asynchronous message passing

Synchronous message passing systems require the sender and receiver to wait for each
other to transfer the message. That is, the sender will not continue until the receiver has
received the message.
Synchronous communication has two advantages. The first advantage is that reasoning
about the program can be simplified in that there is a synchronisation point between
sender and receiver on message transfer. The second advantage is that no buffering is
required. The message can always be stored on the receiving side, because the sender
will not continue until the receiver is ready.
Asynchronous message passing systems deliver a message from sender to receiver,
without waiting for the receiver to be ready. The advantage of asynchronous
communication is that the sender and receiver can overlap their computation because
they do not wait for each other.
Synchronous communication can be built on top of asynchronous communication by
ensuring that the sender always wait for an acknowledgement message from the receiver
before continuing.
The buffer required in asynchronous communication can cause problems when it is full.
A decision has to be made whether to block the sender or whether to discard future
messages. If the sender is blocked, it may lead to an unexpected deadlock. If messages
are dropped, then communication is no longer reliable.

### Message passing versus calling

Message passing should be contrasted with the alternative communication method for
passing information between programs - the Call. In a traditional Call, arguments are
passed to the "callee" ( the receiver) typically by one or more general purpose registers
or in a parameter list containing the addresses of each of the arguments. This form of
communication differs from message passing in at least three crucial areas -
 total memory usage
 transfer time
 locality
In message passing, each of the arguments has to have sufficient available extra
memory for copying the existing argument into a portion of the new message. This
applies irrespective of the size of the original arguments - so if one of the arguments is
( say) an HTML string of 31,000 octets describing a web page ( similar to the size of this
article), it has to be copied in its entirety ( and perhaps even transmitted) to the receiving
program ( if not a local program).
By contrast, for the call method, only an address of say 4 or 8 bytes needs to be passed
for each argument and may even be passed in a general purpose register requiring zero
additional storage and zero "transfer time". This of course is not possible for distributed
systems since an ( absolute) address - in the callers address space - is normally
meaningless to the remote program ( however, a relative address might in fact be usable
if the callee had an exact copy of, at least some of, the callers memory in advance). Web
browsers and web servers are examples of processes that communicate by message
passing. A URL is an example of a way of referencing resources that does depend on
exposing the internals of a process.
A subroutine call or method invocation will not exit until the invoked computation has
terminated. Asynchronous message passing, by contrast, can result in a response
arriving a significant time after the request message was sent.
A message handler is, in general, in receipt of messages from more than one sender.
This means its state can change for reasons unrelated to the behaviour of a single sender
or client process. This is in contrast to the typical behaviour of an object upon which
methods are being invoked: the latter is expected to remain in the same state between
method invocations. ( in other words, the message handler behaves analogously to a
volatile object).

### Message passing and locks

Message passing can be used as a way of controlling access to resources in a concurrent
or asynchronous system. One of the main alternatives is mutual exclusion or locking.
Examples of resources include shared memory, a disk file or region thereof, a database
table or set of rows.
In locking, a resource is essentially shared, and processes wishing to access it ( or a
sector of it) must first obtain a lock. Once the lock is acquired, other processes are
blocked out, ensuring that corruption from simultaneous writes does not occur. The lock
is then released.
With the message-passing solution, it is assumed that the resource is not exposed, and
all changes to it are made by an associated process, so that the resource is encapsulated.
Processes wishing to access the resource send a request message to the handler. If the
resource ( or subsection) is available, the handler makes the requested change as an
atomic event, that is conflicting requests are not acted on until the first request has been
completed. If the resource is not available, the request is generally queued. The sending
programme may or may not wait until the request has been completed.

### Examples of message passing style

 Actor model implementation
 Amorphous computing
 Flow-based programming
 SOAP ( protocol)

### Influences on other programming models

In the terminology of some object-oriented programming languages, a message is the
single means to pass control to an object. If the object "responds" to the message, it has
a method for that message. In pure object-oriented programming, message passing is
performed exclusively through a dynamic dispatch strategy.[citation needed]
Objects can send messages to other objects from within their method bodies. Message
passing enables extreme late binding in systems. Sending the same message to an object
twice will usually result in the object applying the method twice. Two messages are
considered to be the same message type, if the name and the arguments of the message
are identical. Some languages support the forwarding or delegation of method
invocations from one object to another if the former has no method to handle the
message, but "knows" another object that may have one. See also Inversion of Control.
Alan Kay has argued[1] that message passing is more important than objects in OOP,
and that objects themselves are often over-emphasized. The live distributed objects
programming model builds upon this observation; it uses the concept of a distributed
data flow to characterize the behavior of a complex distributed system in terms of
message patterns, using high-level, functional-style specifications.

### See also

 Active message
 Database-centric architecture
 Distributed computing
 Dynamic dispatch
 Event loop
 Inter-process communication
 Message loop in Microsoft Windows
 Message-oriented middleware
 Messaging pattern

### References

1. ^ http://lists.squeakfoundation.org/pipermail/squeak-dev/1998-
October/017019.html

### External links

 Future of Concurrent Programming

### Further reading

 Ramachandran, U.; M. Solomon, M. Vernon ( 1987). "Hardware support for
interprocess communication". Proceedings of the 14th annual international
symposium on Computer architecture. ACM Press.
http://portal.acm.org/citation.cfm?id=30371&coll=&dl=ACM&CFID=1515151
5&CFTOKEN=6184618.
 McQuillan, John M.; David C. Walden ( 1975). "Some considerations for a high
performance message-based interprocess communication system". Proceedings
of the 1975 ACM SIGCOMM/SIGOPS workshop on Interprocess
communications. ACM Press.
http://portal.acm.org/citation.cfm?id=810905&coll=&dl=ACM&CFID=151515
15&CFTOKEN=6184618.
 Shimizu, Toshiyuki; Takeshi Horie, Hiroaki Ishihata ( 1992). "Low-latency
message communication support for the AP1000". Proceedings of the 19th
annual international symposium on Computer architecture. ACM Press.
http://portal.acm.org/citation.cfm?id=140385&coll=&dl=ACM&CFID=151515
15&CFTOKEN=6184618.
Read more: http://www.answers.com/topic/message-passing#ixzz1FdKX6jmZ

## Tuple space

A tuple space is an implementation of the associative memory paradigm for
parallel/distributed computing. It provides a repository of tuples that can be accessed
concurrently. As an illustrative example, consider that there are a group of processors
that produce pieces of data and a group of processors that use the data. Producers post
their data as tuples in the space, and the consumers then retrieve data from the space
that match a certain pattern. This is also known as the blackboard metaphor. Tuple
space may be thought as a form of distributed shared memory.
Tuple spaces were the theoretical underpinning of the Linda language developed by
David Gelernter and Nicholas Carriero at Yale University.
Implementations of tuple spaces have also been developed for Java ( JavaSpaces), Lisp,
Lua, Prolog, Python, Ruby, Smalltalk, Tcl, and the .NET framework.
Contents [hide]
- 1 Object Spaces
- 2 JavaSpaces
  - 2.1 Example usage
  - 2.2 Implementations
  - 2.3 Books
  - 2.4 Interviews
  - 2.5 Articles
- 3 References
- 4 See also
- 5 Sources
- 6 External links

### Object Spaces

Object Spaces is a paradigm for development of distributed computing applications. It
is characterized by the existence of logical entities, called Object Spaces. All the
participants of the distributed application share an Object Space. A provider of a service
encapsulates the service as an Object, and puts it in the Object Space. Clients of a
service then access the Object Space, find out which object provides the needed service,
and have the request serviced by the object.
Object Spaces, as a computing paradigm, was put forward by David Gelernter at Yale
University. Gelernter developed a language called Linda to support the concept of
global object coordination.
Object Space can be thought of as a virtual repository, shared amongst providers and
accessors of network services, which are themselves abstracted as objects. Processes
communicate among each other using these shared objects — by updating the state of
the objects as and when needed.
An object, when deposited into a space, needs to be registered with a Object Directory
in the Object Space. Any processes can then identify the object from the Object
Directory, using properties lookup, where the property specifying the criteria for the
lookup of the object is its name or some other property which uniquely identifies it. A
process may choose to wait for an object to be placed in the Object Space, if the needed
object is not already present.
Objects, when deposited in an Object Space are passive, i.e., their methods cannot be
invoked while the objects are in the Object Space. Instead, the accessing process must
retrieve it from the Object Space into its local memory, use the service provided by the
object, update the state of the object and place it back into the Object Space.
This paradigm inherently provides mutual exclusion. Because once an object is
accessed, it has to be removed from the Object Space, and is placed back only after it
has been released. This means that no other process can access an object while it is
being used by one process, thereby ensuring mutual exclusion.

### JavaSpaces

JavaSpaces is a service specification providing a distributed object exchange and
coordination mechanism ( which may or may not be persistent) for Java objects. It is
used to store the distributed system state and implement distributed algorithms. In a
JavaSpace, all communication partners ( peers) communicate and coordinate by sharing
state.
JavaSpaces can be used to achieve scalability through parallel processing, it can also be
used to provide reliable storage of objects through distributed replication, although this
won't survive a total power failure like a disk; it is regarded by many to be reliable as
long as the power is reliable. Distribution can also be to remote locations; however, this
is rare as JavaSpaces are usually used to low-latency, high performance applications
rather than reliable object caching.
The most common software pattern used in JavaSpaces is the Master-Worker pattern.
The Master hands out units of work to the "space", and these are read, processed and
written back to the space by the workers. In a typical environment there are several
"spaces", several masters and many workers; the workers are usually designed to be
generic, i.e. they can take any unit of work from the space and process the task.
JavaSpaces is part of the Java Jini technology, which on its own has not been a
commercial success. The technology has found and kept new users over the years and
some vendors are offering JavaSpaces-based products. JavaSpaces remains a niche
technology mostly used in the financial services and telco industries where it continues
to maintain a faithful following. The announcement of Jini/JavaSpaces created quite
some hype although Sun co-founder and chief Jini architect Bill Joy put it straight that
this distributed systems dream will take "a quantum leap in thinking".[1]

#### Example usage

The following example shows an application made using JavaSpaces. First, an object to
be shared in the Object Space is made. Such an object is called an Entry in JavaSpace
terminology. Here, the Entry is used to encapsulate a service which returns a Hello
World! string, and keeps track of how many times it was used. The server which
provides this service will create an Object Space, or JavaSpace. The Entry is then
written into the JavaSpace. The client reads the entry from the JavaSpace and invokes
its method to access the service, updating its usage count by doing so. The updated
Entry is written back to the JavaSpace.

```

// An Entry class
public class SpaceEntry implements Entry
{
public final String message = "Hello World!";
public Integer count = 0;
public String service () {
count = count + 1;
return message;
}
public String toString () {
return "Count: " + count;
}
}
// Hello World! server
public class Server
{
public static void main ( String[] args) throws Exception
{
SpaceEntry entry = new SpaceEntry (); // Create the
Entry object
JavaSpace space = ( JavaSpace)space (); // Create an
Object Space
// Register and write the Entry into the Space
space.write ( entry, null, Lease.FOREVER);
// Pause for 10 seconds and then retrieve the Entry and check
its state.
Thread.sleep ( 10*1000);
SpaceEntry e = space.read ( new SpaceEntry (), null,
Long.MAX_VALUE);
System.out.println ( e);
}
}
// Client
public class Client
{
public static void main ( String[] args) throws Exception
{
JavaSpace space = ( JavaSpace) space ();
SpaceEntry e = space.take ( new SpaceEntry (), null,
Long.MAX_VALUE);
System.out.println ( e.service ());
space.write ( e, null, Lease.FOREVER);
}
}

```

#### Implementations

 TIBCO ActiveSpaces, commercial, clustered, fault-tolerant, for Java, C/C++
 The Fly Object Space, for Java, Ruby, Scala
 GigaSpaces, commercial, clustered, fault-tolerant, for Java, .Net, C++
 The Blitz Project, open-source, single site server
 PyLinda for Python
 Rinda for Ruby
 LinuxTuples, open-source, clustered, API for C, Python
 SemiSpace, open-source, clustered with Terracotta Cluster for Java
 SQLSpaces, open-source ( GPL, LGPL), server version in Java, clients for Java,
C#, PHP, Prolog, Ruby
 Linda in a Mobile Environment ( LIME)
 SlackSpaces, open-source, main website down, project source is downloadable
 TSpaces, by IBM for Java, project stalled since 2000

#### Books

 Eric Freeman, Susanne Hupfer, Ken Arnold: JavaSpaces Principles, Patterns,
and Practice. Addison-Wesley Professional, 1. June 1999, ISBN 0-201-30955-6
 Phil Bishop, Nigel Warren: JavaSpaces in Practice. Addison Wesley, 2002,
ISBN 0-321-11231-8
 Max K. Goff: Network Distributed Computing: Fitscapes and Fallacies, 2004,
Prentice Hall, ISBN 0131001523
 Sing Li, et al.: Professional Java Server Programming, 1999, Wrox Press, ISBN
1861002777
 Steven Halter: JavaSpaces Example by Example, 2002, Prentice Hall PTR,
ISBN 0-13-061916-7

#### Interviews

 Gelernter, David ( 2009). "Lord of the Cloud". John Brockman, Editor and
Publisher Russell Weinberger, Associate Publisher, Edge Foundation, Inc.
http://www.edge.org/3rd_culture/gelernter09/gelernter09_index.html.
 Heiss, Janice J. ( 2003). "Computer Visions: A Conversation with David
Gelernter". Sun Developer Network ( SDN).
http://java.sun.com/developer/technicalArticles/Interviews/gelernter_qa.html.
 Venners, Bill ( 2003). "Designing as if Programmers are People ( Interview with
Ken Arnold)". java.net.
http://today.java.net/pub/a/today/2003/06/10/design.html.
 Haines, Steven ( 2006). "Interview: GigaSpaces". InformIT.
http://www.informit.com/guides/content.aspx?g=java&seqNum=263.

#### Articles

 Brogden, William ( 2007). "How Web services can use JavaSpaces".
SearchWebServices.com.
http://searchwebservices.techtarget.com/tip/0,289483,sid26_gci1251765,00.html
. Retrieved 2007-04-18.
 Brogden, William ( 2007). "Grid computing and Web services ( Beowulf,
BOINC, Javaspaces)". SearchWebServices.com.
http://searchwebservices.techtarget.com/tip/0,289483,sid26_gci1248166,00.html
. Retrieved 2007-03-20.
 White, Tom ( 2005). "How To Build a ComputeFarm". java.net.
http://today.java.net/pub/a/today/2005/04/21/farm.html. Retrieved 2005-05-21.
 Ottinger, Joseph ( 2007). "Understanding JavaSpaces". theserverside.
http://www.theserverside.com/tt/articles/article.tss?l=UsingJavaSpaces.
Retrieved 2007-01-31.
 Angerer, Bernhard; Erlacher, Andreas ( 2005). "Loosely Coupled
Communication and Coordination in Next-Generation Java Middleware".
java.net. http://today.java.net/pub/a/today/2005/06/03/loose.html. Retrieved
2006-06-03.
 Angerer, Bernhard ( 2003). "Space-Based Programming". onjava.com.
http://www.onjava.com/pub/a/onjava/2003/03/19/java_spaces.html. Retrieved
2003-03-19.
 Sing, Li ( 2003). "High-impact Web tier clustering, Part 2: Building adaptive,
scalable solutions with JavaSpaces". IBM developerworks. http://www-
128.ibm.com/developerworks/java/library/j-cluster2/?Open&ca=daw-co-news.
 Mamoud,, Qusay H. ( 2005). "Getting Started With JavaSpaces Technology:
Beyond Conventional Distributed Programming Paradigms". Sun Developer
Network ( SDN).
http://java.sun.com/developer/technicalArticles/tools/JavaSpaces/.
 Hupfer, Susanne ( 1999). "Make room for Javaspaces, Part 1 ( from 5)".
JavaWorld. http://www.javaworld.com/javaworld/jw-11-1999/jw-11-
jiniology.html.
 Löffler, Dr. Gerald ( 2004). "JavaSpaces und ihr Platz im Enterprise Java
Universum, Das Modell zum Objektaustausch: JavaSpaces vorgestellt".
Entwickler.com.
http://www.javamagazin.de/itr/online_artikel/psecom,id,489,nodeid,11.html.
Retrieved 2004-02-01.
 Shalom, Nati ( 2006). "Space-Based Architecture and the End of Tier-Based
Computing". GigaSpaces Technologies.
http://www.gigaspaces.com/os_papers.html#a1.
 Arango, Mauricio ( 2009). "Coordination in parallel event-based systems".
blogs.sun.com.
http://blogs.sun.com/arango/entry/coordination_in_parallel_event_based.

### References

1. ^ Rob Guth: "More than just another pretty name: Sun's Jini opens up a new
world of distributed computer systems". SunWorld, August 1998 [15 January
2006]

### See also

 Space-based architecture
 Linda ( coordination language)
 Ken Arnold, lead engineer on JavaSpaces at Sun Microsystems
 Rinda, a JavaSpaces analog for Ruby

### Sources

 Gelernter, David. "Generative communication in Linda". ACM Transactions on
Programming Languages and Systems, volume 7, number 1, January 1985
 Distributed Computing ( First Indian reprint, 2004), M. L. Liu

### External links

 "TupleSpace" at c2.com
 "JavaSpace Specification" at jini.org
Read more: http://www.answers.com/topic/tuple-space#ixzz1FdKqLe8D

## Atomicity

In concurrent programming, an operation ( or set of operations) is atomic, linearizable,
indivisible or uninterruptible if it appears to the rest of the system to occur
instantaneously. Atomicity is a guarantee of isolation from concurrent processes.
Additionally, atomic operations commonly have a succeed-or-fail definition — they
either successfully change the state of the system, or have no visible effect.
Atomicity is commonly enforced by mutual exclusion, whether at the hardware level
building on a cache coherency protocol, or the software level using semaphores or
locks. Thus, an atomic operation does not actually occur instantaneously. The benefit
comes from the appearance: the system behaves as if each operation occurred instantly,
separated by pauses. Because of this, implementation details may be ignored by the
user, except insofar as they affect performance. If an operation is not atomic, the user
will also need to understand and cope with sporadic extraneous behaviour caused by
interactions between concurrent operations, which by its nature is likely to be hard to
reproduce and debug.
Contents [hide]
- 1 Primitive atomic instructions
- 2 High-level atomic operations
- 3 Example atomic operation
  - 3.1 Non-atomic
  - 3.2 Compare-and-swap
  - 3.3 Locking
- 4 History of linearizability
- 5 Definition of linearizability
  - 5.1 Linearizability versus serializability
  - 5.2 Linearization points
- 6 Strict consistency
- 7 See also
- 8 References

### Primitive atomic instructions

Most modern processors have instructions which can be used to implement locking and
lock-free and wait-free algorithms. The ability to temporarily turn off interrupts,
ensuring that the currently running process cannot be context switched, also suffices on
a uniprocessor. These instructions are used directly by compiler and operating system
writers but are also abstracted and exposed as bytecodes and library functions in higher-
level languages.
 Atomic read and write
 Atomic swap as used in some Burroughs mainframes, also called XCHG.
 Test-and-set
 Fetch-and-add
 Compare-and-swap
 Load-Link/Store-Conditional
Many of these primitives can be implemented in terms of each other.
Many processors, especially 32-bit ones with 64-bit floating point support, also provide
some read and write operations that are not atomic: one thread reading a 64-bit register
while another thread is writing to it may see a combination of both "before" and "after"
values, a combination that may never actually have been written to the register. Further,
only single operations are guaranteed to be atomic; threads arbitrarily performing
groups of reads and writes will also observe a mixture of "before" and "after" values.

### High-level atomic operations

The easiest way to achieve linearizability is running groups of primitive operations in a
critical section. Strictly independent operations can then be carefully permitted to
overlap their critical sections, provided this does not violate linearizability. Such an
approach must balance the cost of large numbers of locks against the benefits of
increased parallelism.
Another approach, favoured by researchers ( but not yet widely used in the software
industry), is to design a linearizable object using the native atomic primitives provided
by the hardware. This has the potential to maximise available parallelism and minimise
synchronisation costs, but requires mathematical proofs which show that the objects
behave correctly.
A promising hybrid of these two is to provide a transactional memory abstraction. As
with critical sections, the user marks sequential code that must be run in isolation from
other threads. The implementation then ensures the code executes atomically. This style
of abstraction is common when interacting with databases; for instance, when using the
Spring Framework, annotating a method with @Transactional will ensure all enclosed
database interactions occur in a single database transaction. Transactional memory goes
a step further, ensuring that all memory interactions occur atomically. As with database
transactions, issues arise regarding composition of transactions, especially database and
in-memory transactions.
A common theme when designing linearizable objects is to provide an all-or-nothing
interface: either an operation succeeds completely, or it fails and does nothing. ( ACID
databases refer to this principle as atomicity.) If the operation fails ( usually due to
concurrent operations), the user must retry, usually performing a different operation. For
example:
 Compare-and-swap writes a new value into a location only if it matches a
supplied old value. This is commonly used in a read-modify-CAS sequence: the
user reads the location, computes a new value to write, and writes it with a CAS;
if the value changes concurrently, the CAS will fail and the user tries again.
 Load-Link/Store-Conditional encodes this pattern more directly: the user reads
the location with load-link, computes a new value to write, and writes it with
store-conditional; if the value has changed concurrently, the SC will fail and the
user tries again.
 In a database transaction, if the transaction cannot be completed due to a
concurrent operation ( e.g. in a deadlock), the transaction will be aborted and the
user must try again.

### Example atomic operation

Consider a simple counter which different processes can increment.

#### Non-atomic

The naive, non-atomic implementation:
1. reads the value in the memory location;
2. adds one to the value;
3. writes the new value back into the memory location.
Now, imagine two processes are running incrementing a single, shared memory
location:
1. the first process reads the value in memory location;
2. the first process adds one to the value;
but before it can write the new value back to the memory location it is suspended, and
the second process is allowed to run:
1. the second process reads the value in memory location, the same value that the
first process read;
2. the second process adds one to the value;
3. the second process writes the new value into the memory location.
The second process is suspended and the first process allowed to run again:
1. the first process writes a now-wrong value into the memory location, unaware
that the other process has already updated the value in the memory location.
This is a trivial example. In a real system, the operations can be more complex and the
errors introduced extremely subtle. For example, reading a 64-bit value from memory
may actually be implemented as two sequential reads of two 32-bit memory locations. If
a process has only read the first 32 bits, and before it reads the second 32 bits the value
in memory gets changed, it will have neither the original value nor the new value but a
mixed-up garbage value.
Furthermore, the specific order in which the processes run can change the results,
making such an error difficult to detect, reproduce and debug.

#### Compare-and-swap

Most systems provide an atomic compare-and-swap instruction that reads from a
memory location, compares the value with an "expected" one provided by the user, and
writes out a "new" value if the two match, returning whether the update succeeded. We
can use this to fix the non-atomic counter algorithm as follows:
1. read the value in the memory location;
2. add one to the value
3. use compare-and-swap to write the incremented value back
4. retry if the value read in by the compare-and-swap did not match the
value we originally read
Since the compare-and-swap occurs ( or appears to occur) instantaneously, if another
process updates the location while we are in-progress, the compare-and-swap is
guaranteed to fail.

#### Locking

Main article: Lock ( computer science)
Another approach is to turn the naive algorithm into a critical section, preventing other
threads from disrupting it, using a lock. Once again fixing the non-atomic counter
algorithm:
1. take a lock, excluding other threads from running the critical section
( steps 2-4) at the same time
2. read the value in the memory location
3. add one to the value
4. write the incremented value back to the memory location
5. release the lock
This strategy works with any problem; compared with direct use of atomic operations, it
is relatively easy to get right, but it requires great care to not suffer significant overhead.
To improve program performance, it may therefore be a good idea to replace simple
critical sections with atomic operations for non-blocking synchronization ( as we have
just done for the counter with compare-and-swap), instead of the other way around, but
unfortunately a significant improvement is not guaranteed and lock-free algorithms can
easily become too complicated to be worth the effort.

### History of linearizability

Linearizability was first introduced as a consistency model by Herlihy and Wing in
1987. It encompassed more restrictive definitions of atomic, such as "an atomic
operation is one which cannot be ( or is not) interrupted by concurrent operations",
which are usually vague about when an operation is considered to begin and end.
An atomic object can be understood immediately and completely from its sequential
definition, as a set of operations run in parallel will always appear to occur one after the
other; no inconsistencies may emerge. Specifically, linearizability guarantees that the
invariants of a system are observed and preserved by all operations: if all operations
individually preserve an invariant, the system as a whole will.

### Definition of linearizability

A history is a sequence of invocations and responses made of an object by a set of
threads. Each invocation of a function will have a subsequent response. This can be
used to model any use of an object. Suppose, for example, that two threads, A and B,
both attempt to grab a lock, backing off if it's already taken. This would be modeled as
both threads invoking the lock operation, then both threads receiving a response, one
successful, one not.
A invokes lock B invokes lock A gets "failed" response B gets "successful" response
A sequential history is one in which all invocations have immediate responses. A
sequential history should be trivial to reason about, as it has no real concurrency; the
previous example was not sequential, and thus is hard to reason about. This is where
linearizability comes in.
A history is linearizable if:
 its invocations and responses can be reordered to yield a sequential history
 that sequential history is correct according to the sequential definition of the
object
 if a response preceded an invocation in the original history, it must still precede
it in the sequential reordering
( Note that the first two bullet points here match serializability: the operations appear to
happen in some order. It is the last point which is unique to linearizability, and is thus
the major contribution of Herlihy and Wing.)
Let us look at two ways of reordering the locking example above.
A invokes lock A gets "failed" response B invokes lock B gets "successful" response
Reordering B's invocation below A's response yields a sequential history. This is easy to
reason about, as all operations now happen in an obvious order. Unfortunately, it doesn't
match the sequential definition of the object: A should have successfully obtained the
lock, and B should have subsequently aborted.
B invokes lock B gets "successful" response A invokes lock A gets "failed" response
This is another correct sequential history. It is also a linearization! Note that the
definition of linearizability only precludes responses that precede invocations from
being reordered; since the original history had no responses before invocations, we can
reorder it as we wish. Hence the original history is indeed linearizable.
An object ( as opposed to a history) is linearizable if all valid histories of its use can be
linearized. Note that this is a much harder assertion to prove.

#### Linearizability versus serializability

Consider the following history, again of two objects interacting with a lock:
A invokes A successfully B invokes B successfully A invokes A successfully
lock locks unlock unlocks unlock unlocks
This history is visibly not linearizable, as it cannot be reordered to another sequential
history without violating the ordering rule. However, under serializability, we may
reorder B's unlock operation to before A's original lock, which is a valid history
assuming the object begins the history in a locked state:
B invokes B successfully A invokes A successfully A invokes A successfully
unlock unlocks lock locks unlock unlocks
While weird, this reordering is sensible provided there is no alternative means of
communicating between A and B. Linearizability is better when considering individual
objects separately, as the reordering restrictions ensure that multiple linearizable objects
are, considered as a whole, still linearizable.

#### Linearization points

This definition of linearizability is equivalent to the following:
 All function calls have a linearization point at some instant between their
invocation and their response
 All functions appear to occur instantly at their linearization point, behaving as
specified by the sequential definition
This alternative is usually much easier to prove. It is also much easier to reason about as
a user, largely due to its intuitiveness. This property of occurring instantaneously, or
indivisibly, leads to the use of the term atomic as an alternative to the longer
"linearizable".
In the examples above, the linearization point of the counter built on CAS is the
linearization point of the first ( and only) successful CAS update. The counter built using
locking can be considered to linearize at any moment while the locks are held, since any
potentially conflicting operations are excluded from running during that period.

### Strict consistency

Strict consistency in computer science is the most stringent consistency model. It says
that a read operation has to return the result of the latest write operation which occurred
on that data item.

### See also

 Atomic transaction
 Consistency model
 ACID

### References

 M. Herlihy and J. Wing, "Axioms for Concurrent Objects", Proceedings of the
14th ACM SIGACT-SIGPLAN symposium on Principles of programming
languages ( January 1987), pp. 13-26 [1].
 M. Herlihy, "A methodology for implementing highly concurrent data
structures", ACM SIGPLAN symposium on Principles & practice of parallel
programming, 1990, pp. 197-206 [2].
 M. Herlihy and J.Wing "Linearizability: a correctness condition for concurrent
objects", ACM Transactions on Programming Languages and Systems, 1990,
pp. 463-492 [3].
Read more: http://www.answers.com/topic/linearizability#ixzz1FdLBwEeO

## Concurrency control

In information technology and computer science, especially in the fields of computer
programming ( see also concurrent programming, parallel programming), operating
systems ( see also parallel computing), multiprocessors, and databases, concurrency
control ensures that correct results for concurrent operations are generated, while
getting those results as quickly as possible.
Computer systems, both software and hardware, consist of modules, or components.
Each component is designed to operate correctly, i.e., to obey to or meet certain
consistency rules. When components that operate concurrently interact by messaging or
by sharing accessed data ( in memory or storage), a certain component's consistency may
be violated by another component. The general area of concurrency control provides
rules, methods, design methodologies, and theories to maintain the consistency of
components operating concurrently while interacting, and thus the consistency and
correctness of the whole system. Introducing concurrency control into a system means
applying operation constraints which typically result in some performance reduction.
Operation consistency and correctness should be achieved with as good as possible
efficiency, without reducing performance below reasonable.
See also Concurrency ( computer science).
Contents [hide]

- 1 Concurrency control in databases
  - 1.1 Database transaction and the ACID rules
  - 1.2 Why is concurrency control needed?
  - 1.3 Concurrency control mechanisms
    - 1.3.1 Types of mechanisms
    - 1.3.2 Major goals
      - 1.3.2.1 Serializability
      - 1.3.2.2 Recoverability
      - 1.3.2.3 Distribution: Distributed serializability and Commitment ordering
  - 1.4 See also
  - 1.5 References
- 2 Concurrency control in operating systems
  - 2.1 See also
  - 2.2 References

### Concurrency control in databases

Comments:
1. This section is applicable to all transactional systems, i.e., to all systems that use
database transactions ( atomic transactions; e.g., transactional objects in Systems
management and in networks of smartphones), not only database management
systems ( DBMSs).
2. DBMSs need to deal also with concurrency control issues not typical just to database
transactions but rather to operating systems in general. These issues ( e.g., see
Concurrency control in operating systems below) are out of the scope of this section.
Concurrency control in Database management systems ( DBMS; e.g., Bernstein et al.
1987, Weikum and Vossen 2001), other transactional objects, and related distributed
applications ( e.g., Grid computing and Cloud computing) ensures that database
transactions are performed concurrently without violating the data integrity of the
respective databases. Thus concurrency control is an essential element for correctness in
any system where two database transactions or more, executed with time overlap, can
access the same data, e.g., virtually in any general-purpose database system.
Consequently a vast body of related research has been accumulated since database
systems have emerged in the early 1970s. A well established concurrency control theory
exists for database systems: serializability theory, which allows to effectively design
and analyze concurrency control methods and mechanisms.
To ensure correctness, a DBMS usually guarantees that only serializable transaction
schedules are generated, unless serializability is intentionally relaxed to increase
performance, but only in cases that application correctness is not harmed. For
maintaining correctness in cases of failed ( aborted) transactions ( which can always
happen for many reasons) schedules also need to have the recoverability property. A
DBMS also guarantees that no effect of committed transactions is lost, and no effect of
aborted ( rolled back) transactions remains in the related database. Overall transaction
characterization is usually summarized by the ACID rules below. As databases become
distributed, or cooperate in distributed environments ( e.g., Cloud computing), the
effective distribution of concurrency control mechanisms receives special attention.

#### Database transaction and the ACID rules

Main articles: Database transaction and ACID
The concept of a database transaction ( or atomic transaction) has evolved in order to
enable both a well understood database system behavior in a faulty environment where
crashes can happen any time, and recovery from a crash to a well understood database
state. A database transaction is a unit of work, typically encapsulating a number of
operations over a database ( e.g., reading a database object, writing, acquiring lock, etc.),
an abstraction supported in database and also other systems. Each transaction has well
defined boundaries in terms of which program/code executions are included in that
transaction ( determined by the transaction's programmer via special transaction
commands). Every database transaction obeys the following rules ( by support in the
database system; i.e., a database system is designed to guarantee them for the
transactions it runs):
 Atomicity - Either the effects of all or none of its operations remain ("all or nothing"
semantics) when a transaction is completed ( committed or aborted respectively). In
other words, to the outside world a committed transaction appears ( by its effects) to
be indivisible, atomic, and an aborted transaction does not leave effects at all, as if
never existed.
 Consistency - Every transaction must leave the database in a consistent ( correct) state,
i.e., maintain the predetermined integrity rules of the database ( constraints upon and
among the database's objects). A transaction must transform a database from one
consistent state to another consistent state ( it is the responsibility of the transaction's
programmer to make sure that the transaction itself is correct, i.e., performs correctly
what it intends to perform while maintaining the integrity rules). Thus since a database
can be normally changed only by transactions, all the database's states are consistent.
An aborted transaction does not change the state.
 Isolation - Transactions cannot interfere with each other. Moreover, usually the
effects of an incomplete transaction are not visible to another transaction. Providing
isolation is the main goal of concurrency control.
 Durability - Effects of successful ( committed) transactions must persist through
crashes ( typically by recording the transaction's effects and its commit event in a non-
volatile memory).

#### Why is concurrency control needed?

If transactions are executed serially, i.e., sequentially with no overlap in time, no
transaction concurrency exists. However, if concurrent transactions with interleaving
operations are allowed in an uncontrolled manner, some unexpected, undesirable result
may occur. Here are some typical examples:
1. The lost update problem: A second transaction writes a second value of a data-item
( datum) on top of a first value written by a first concurrent transaction, and the first
value is lost to other transactions running concurrently which need, by their
precedence, to read the first value. The transactions that have read the wrong value
end with incorrect results.
2. The dirty read problem: Transactions read a value written by a transaction that has
been later aborted. This value disappears from the database upon abort, and should
not have been read by any transaction ("dirty read"). The reading transactions end
with incorrect results.
3. The incorrect summary problem: While one transaction takes a summary over the
values of all the instances of a repeated data-item, a second transaction updates some
instances of that data-item. The resulting summary does not reflect a correct result for
any ( usually needed for correctness) precedence order between the two transactions
( if one is executed before the other), but rather some random result, depending on
the timing of the updates, and whether certain update results have been included in
the summary or not.

#### Concurrency control mechanisms

##### Types of mechanisms

The main categories of concurrency control mechanisms are:
 Optimistic - Delay the checking of whether a transaction meets the isolation and other
integrity rules ( e.g., serializability and recoverability) until its end, without blocking any
of its ( read, write) operations ("...and be optimistic about the rules being met..."), and
then abort a transaction to prevent the violation, if the desired rules are to be violated
upon its commit. An aborted transaction is immediately restarted and re-executed,
which incurs an obvious overhead ( versus executing it to the end only once). If not too
many transactions are aborted, then being optimistic is usually a good strategy.
 Pessimistic - Block an operation of a transaction, if it may cause violation of the rules,
until the possibility of violation disappears. Blocking operations is typically involved
with performance reduction.
 Semi-optimistic - Block operations in some situations, if they may cause violation of
some rules, and do not block in other situations while delaying rules checking to
transaction's end, as done with optimistic.
Different categories provide different performance, i.e., different average transaction
completion rates ( throughput), depending on transaction types mix, computing level of
parallelism, and other factors. If selection and knowledge about trade-offs are available,
then category and method should be chosen to provide the highest performance.
Many methods for concurrency control exist. Most of them can be implemented within
either main category above. The major methods, which have each many variants, and in
some cases may overlap or be combined, are:
1. Locking ( e.g., Two-phase locking - 2PL) - Controlling access to data by locks assigned to
the data. Access of a transaction to a data item ( database object) locked by another
transaction may be blocked ( depending on lock type and access operation type) until
lock release.
2. Serialization graph checking ( also called Serializability, or Conflict, or Precedence
graph checking) - Checking for cycles in the schedule's graph and breaking them by
aborts.
3. Timestamp ordering ( TO) - Assigning timestamps to transactions, and controlling or
checking access to data by timestamp order.
4. Commitment ordering ( or Commit ordering; CO) - Controlling or checking transactions'
order of commit events to be compatible with their respective precedence order.
Other major concurrency control types that are utilized in conjunction with the methods
above include:
 Multiversion concurrency control ( MVCC) - Increasing concurrency and performance
by generating a new version of a database object each time the object is written, and
allowing transactions' read operations of several last relevant versions ( of each object)
depending on scheduling method.
 Index concurrency control - Synchronizing access operations to indexes, rather than to
user data. Specialized methods provide substantial performance gains.
The most common mechanism type in database systems since their early days in the
1970s has been Strong strict Two-phase locking ( SS2PL; also called Rigorous
scheduling or Rigorous 2PL) which is a special case ( variant) of both Two-phase
locking ( 2PL) and Commitment ordering ( CO). It is pessimistic. In spite of its long
name ( for historical reasons) the idea of the SS2PL mechanism is simple: "Release all
locks applied by a transaction only after the transaction has ended." SS2PL ( or
Rigorousness) is also the name of the set of all schedules that can be mechanism, i.e., these are SS2PL ( or Rigorous) schedules, have the SS2PL ( or
Rigorousness) property.

##### Major goals

Concurrency control mechanisms are usually designed to achieve some of, or all the
following goals:

###### Serializability

Main article: Serializability
For correctness, a common major goal of most concurrency control mechanisms is
generating schedules with the Serializability property. Without serializability
undesirable phenomena may occur, e.g., money may disappear from accounts, or be
generated from nowhere. Serializability of a schedule means equivalence ( in the
resulting database values) to some serial schedule with the same transactions ( i.e., in
which transactions are sequential with no overlap in time, and thus completely isolated
from each other: No concurrent access by any two transactions to the same data is
possible). Serializability is considered the highest level of isolation among database
transactions, and the major correctness criterion for concurrent transactions. In some
cases compromised, relaxed forms of serializability are allowed for better performance
( e.g., the popular Snapshot isolation mechanism), if application's correctness is not
violated by the relaxation.
Almost all implemented concurrency control mechanisms achieve serializability by
providing Conflict serializablity, a broad special case of serializability ( i.e., it covers,
enables most serializable schedules, and does not impose significant additional delay-
causing constraints) which can be implemented efficiently.

###### Recoverability

See Recoverability in Serializability
Concurrency control typically also ensures the Recoverability property of schedules for
maintaining correctness in cases of aborted transactions ( which can always happen for
many reasons). Recoverability means that no committed transaction in a schedule has
read data written by an aborted transaction. Such data disappear from the database
( upon the abort) and are parts of an incorrect database state. Reading such data violates
the consistency rule of ACID. Unlike Serializability, Recoverability cannot be
compromised, relaxed at any case, since any relaxation results in quick database
integrity violation upon aborts. The major mechanisms listed above are serializability
mechanisms. None of them in its general form automatically provides recoverability,
and special considerations and mechanism enhancements are needed to support
recoverability. A commonly utilized special case of recoverability is Strictness, which
allows efficient database recovery from failure ( but excludes optimistic
implementations; e.g, Strict CO ( SCO) does not not allow an optimistic implementation,
but allows semi-optimistic).
Comment: Note that the Recoverability property is needed even if no database failure
occurs and no database recovery from failure is needed. It is rather needed to correctly
automatically handle transaction aborts, which may be unrelated to database failure and
recovery from it.

###### Distribution: Distributed serializability and Commitment ordering

See Distributed serializability in Serializability
Main article: Global serializability
Main article: Commitment ordering
As database systems become distributed, or cooperate in distributed environments ( e.g.,
in Grid computing, Cloud computing, and networks with smartphones), transactions
may become distributed. A distributed transaction means that the transaction spans
processes, and may span computers and geographical sites. This generates a need in
effective distributed concurrency control mechanisms. Achieving the Serializability
property of a distributed system's schedule ( see Distributed serializability and Global
serializability ( Modular serializability)) effectively poses special challenges typically
not met by most of the regular serializability mechanisms, originally designed to operate
locally. This is especially due to a need in costly distribution of concurrency control
information amid communication and computer latency. The only known general
effective technique for distribution is Commitment ordering, which was disclosed
publicly in 1991 ( after being patented). Commitment ordering ( Commit ordering, CO;
Raz 1992) means that transactions' order of commit events is kept compatible with their
respective precedence order. CO does not require the distribution of concurrency control
information and provides a general effective solution ( reliable, high-performance, and
scalable) for both distributed and global serializability, also in a heterogeneous
environment with database systems ( or other transactional objects) with different ( any)
concurrency control mechanisms. CO is indifferent to which mechanism is utilized,
since it does not interfere with any transaction operation scheduling ( which most
mechanisms control), and only determines the order of commit events. Thus, CO
enables the efficient distribution of all other mechanisms, and also the distribution of a
mix of different ( any) local mechanisms, for achieving distributed and global
serializability. The existence of such a solution has been considered "unlikely" until
1991, and by many experts also later, due to misunderstanding of the CO solution ( see
Quotations in Global serializability). An important side-benefit of CO is automatic
distributed deadlock resolution. Contrary to CO, virtually all other techniques ( without
CO) are prone to distributed deadlocks ( also called global deadlocks) which need
special handling. CO is also the name of the resulting schedule property: A schedule has
the CO property if the chronological order of its transactions' commit events is
compatible with the respective transactions' precedence ( partial) order.
SS2PL mentioned above is a variant ( special case) of CO and thus also effective to
achieve distributed and global serializability. It also provides automatic distributed
deadlock resolution ( a fact overlooked in the research literature even after CO's
publication), as well as Strictness and thus Recoverability. Possessing these desired
properties together with known efficient locking based implementations explains
SS2PL's popularity. SS2PL has been utilized to efficiently achieve Distributed and
Global serializability since the 1980, and has become the de-facto standard for it.
However, SS2PL is blocking and constraining ( pessimistic), and with the proliferation
of distribution and utilization of systems different from traditional database systems
( e.g., as in Cloud computing), less constraining types of CO ( e.g., Optimistic CO) may
be needed for better performance.
Comments:
1. The Distributed conflict serializability property in its general form is difficult to achieve
efficiently, but it is achieved efficiently via its special case Distributed CO: Each local
component ( e.g., a local DBMS) needs both to provide some form of CO, and enforce a
special voting strategy for the Two-phase commit protocol ( 2PC: utilized to commit
distributed transactions). Unlike Serializability, Distributed recoverability and
Distributed strictness can be achieved efficiently in a straightforward way ( Raz 1992,
page 307), similarly to the way Distributed CO is achieved ( applied locally with similar
voting strategies). Differently from the general Distributed CO, Distributed SS2PL exists
automatically when all local components are SS2PL based ( in each component CO
exists, implied, and the voting strategy is now met automatically). This fact has been
known and utilized since the 1980s ( i.e., that SS2PL exists globally, without knowing
about CO) for efficient Distributed SS2PL, which implies Distributed serializability and
strictness ( e.g., see Raz 1992, page 293; it is also implied in Bernstein et al. 1987, page
78). Less constrained Distributed serializability and strictness can be efficiently
achieved by Distributed Strict CO ( SCO), or by a mix of SS2PL based and SCO based
local components.
2. About the references and Commitment ordering: ( Bernstein et al. 1987) was published
before the discovery of CO in 1990. CO is described in ( Weikum and Vossen 2001,
pages 102, 700), but the description is partial and misses CO's essence. ( Raz 1992) was
the first refereed and accepted for publication article about CO. Other CO articles
followed.

#### See also

 Schedule
 Isolation ( computer science)
 Distributed concurrency control
 Global concurrency control

#### References

 Philip A. Bernstein, Vassos Hadzilacos, Nathan Goodman ( 1987): Concurrency Control
and Recovery in Database Systems ( free PDF download), Addison Wesley Publishing
Company, 1987, ISBN 0-201-10715-5
 Gerhard Weikum, Gottfried Vossen ( 2001): Transactional Information Systems,
Elsevier, ISBN 1-55860-508-8
 Yoav Raz ( 1992): "The Principle of Commitment Ordering, or Guaranteeing
Serializability in a Heterogeneous Environment of Multiple Autonomous Resource
Managers Using Atomic Commitment." ( PDF), Proceedings of the Eighteenth
International Conference on Very Large Data Bases ( VLDB), pp. 292-312, Vancouver,
Canada, August 1992. ( also DEC-TR 841, Digital Equipment Corporation, November
1990)

### Concurrency control in operating systems

This section requires expansion.
Multitasking operating systems, especially real-time operating systems, need to
maintain the illusion that all tasks running on top of them are all running at the same
time, even though only one or a few tasks really are running at any given moment due
to the limitations of the hardware the operating system is running on. Such multitasking
is fairly simple when all tasks are independent from each other. However, when several
tasks try to use the same resource, or when tasks try to share information, it can lead to
confusion and inconsistency. The task of concurrent computing is to solve that problem.
Some solutions involve "locks" similar to the locks used in databases, but they risk
causing problems of their own such as deadlock. Other solutions are Non-blocking
algorithms.

#### See also

 Linearizability
 Mutual exclusion
 Semaphore ( programming)
 Lock ( computer science)
 Software transactional memory

#### References

 Andrew S. Tanenbaum, Albert S Woodhull ( 2006): Operating Systems Design and
Implementation, 3rd Edition, Prentice Hall, ISBN 0-131-42938-8
 Silberschatz, Avi; Galvin, Peter; Gagne, Greg ( 2008). Operating Systems Concepts, 8th
edition. John Wiley & Sons. ISBN 0-470-12872-0.
Read more: http://www.answers.com/topic/concurrency-control#ixzz1FdLW5jei

## Mutually exclusive events

In layman's terms, two events are mutually exclusive if they cannot occur at the same
time ( i.e., they have no common outcomes). An example is tossing a coin, which can
result in either heads or tails, but not both. Both outcomes cannot happen
simultaneously. Incidentally, both outcomes are collectively exhaustive, which means
that at least one of the outcomes must happen ( ignoring the possibility that the coin will
land on its edge). Not all mutually exclusive events are collectively exhaustive. For
example, the outcomes 1 and 4 of rolling a six-sided die are mutually exclusive ( cannot
happen at the same time) but not collectively exhaustive ( there are other possible
outcomes).
Contents

- 1 Logic
- 2 Probability
- 3 Statistics
- 4 See also
- 5 Notes
- 6 References

### Logic

In logic, two mutually exclusive propositions are propositions that logically cannot
both be true. Another term for mutually exclusive is "disjoint." To say that more than
two propositions are mutually exclusive may, depending on context mean that no two of
them can both be true, or only that they cannot all be true. The term pairwise mutually
exclusive always means no two of them can both be true ever.

### Probability

In probability theory, events E , E , ..., E are said to be mutually exclusive if the
1 2 n
occurrence of any one of them automatically implies the non-occurrence of the
remaining n − 1 events. Therefore, two mutually exclusive events cannot both occur.
Mutually exclusive events have the property: P ( A ∩ B) = 0.[1] For example, one cannot
draw a card that is both red and a club because clubs are always black. If one draws just
one card from the deck, either a red card or a club can be drawn. When A and B are
mutually exclusive, P ( A or B) = P ( A) + P ( B).[2] One might ask, "What is the probability
of drawing a red card or a club?" This problem would be solved by adding together the
probability of drawing a red card and the probability of drawing a club. In a standard
52-card deck, there are twenty-six red cards and thirteen clubs: 26/52 + 13/52 = 39/52
or 3/4.
One would have to draw at least two cards in order to draw both a red card and a club.
The probability would depend on whether the first card were replaced. The probabilities
would be multiplied rather than added. Without replacement, there would be one fewer
card after the first card was drawn. The probability of drawing the two cards would be
26/52 * 13/51 = 338/2652, or 13/102. With replacement, the probability would be 26/52
- 13/52 = 338/2704, or 13/104.
When events are not mutually exclusive, the word "or" allows for the possibility of both
events happening. If they are inclusive events ( i.e., non-mutually exclusive events), P ( A
or B) = P ( A) + P ( B) – P ( A and B).[2] Therefore, if one asks, "What is the probability of
drawing a red card or a king?" drawing a red king is considered a success. In a standard
52-card deck, there are twenty-six red cards and four kings, two of which are red: 26/52
- 4/52 – 2/52 = 28/52.
Events are collectively exhaustive if all the possibilities for outcomes are exhausted, and
at least one of those outcomes must occur. The probability that at least one of the events
will occur is equal to 1.[3] For example, there are theoretically only two possibilities for
flipping a coin. Flipping a head and flipping a tail are collectively exhaustive events,
and there is a probability of 1 of flipping either a head or a tail. Events can be both
mutually exclusive and collectively exhaustive.[3] In the case of flipping a coin, flipping
a head and flipping a tail are also mutually exclusive events. Both outcomes cannot
occur for a single trial ( i.e., when a coin is flipped only once). The probability of
flipping a head and the probability of flipping a tail can be added to yield a probability
of 1: 1/2 + 1/2 =1.[4]

### Statistics

In statistics, each observation should be mutually exclusive in order for them to be
properly differentiated and organized into separate categories, ( such as male and
female). Unlike in logic, however, of the two mutually exclusive observations, one does
not necessarily have to be false. They both can be true, just not at the same time in the
same category, ( statistically speaking, a person cannot be both male and female, but two
different people can be). In fact, the textbook definition of mutually exclusive from a
statistics perspective is, "A property of a set of categories such that an individual or
object is included in only one category."[5] Another definition from the same source also
says, "The occurrence of one event means that none of the other events can occur at the
same time."[6] Essentially, in statistics the concept of something being mutually
exclusive serves to prevent it from being counted more than once in the overall tally and
has less to do with it being true or false over something else ( although it is always
preferable to count only true data)....

### See also

 Collectively exhaustive
 Bounded rationality
 Dichotomy
 Game theory
 Holarchy
 In-joke
 Polytely – problem-solving situations characterized by the presence of several
goals
 Synchronicity

### Notes

1. ^ Mutually Exclusive Events. Interactive Mathematics. December 28, 2008.
2. ^
a b
Stats: Probability Rules.
3. ^
a b
Scott Bierman. A Probability Primer. Carleton College. Pages 3-4.
4. ^ Non-Mutually Exclusive Outcomes. CliffsNotes.
5. ^ Chapter One Outline. McGraw-Hill Higher Education.
6. ^ Chapter Five Outline. McGraw-Hill Higher Education.

### References

 The Analysis of Biological Data, Michael C. Whitlock and Dolph Schluter.
 Basic Statistics for Business & Economics, 4th edition, written by doctors
Douglas A. Lind, William G. Marchal, and Samuel A. Wathen.
Read more: http://www.answers.com/topic/mutually-exclusive-events-1#ixzz1FdLqkghx

## Dining philosophers problem

In computer science, the dining philosophers problem is an illustrative example of a
common computing problem in concurrency. It is a classic multi-process
synchronization problem.
In 1965, Edsger Dijkstra set an examination question on a synchronization problem
where five computers competed for access to five shared tape drive peripherals. Soon
afterwards the problem was retold by Tony Hoare as the dining philosophers
problem.[1][2]
This is a theoretical explanation of deadlock and resource starvation by assuming that
each philosopher takes a different fork as a first priority and then looks for another.
Contents

- 1 Problem
  - 1.1 Issues
- 2 Solutions
  - 2.1 Conductor solution
  - 2.2 Resource hierarchy solution
  - 2.3 Monitor solution
  - 2.4 Chandy / Misra solution
- 3 Example solution
- 4 See also
- 5 References
- 6 External links

### Problem

The dining philosophers problem is summarized as five silent philosophers sitting at a
circular table doing one of two things: eating or thinking. While eating, they are not
thinking, and while thinking, they are not eating. A large bowl of spaghetti is placed in
the center, which requires two forks to serve and to eat ( the problem is therefore
sometimes explained using rice and chopsticks rather than spaghetti and forks). A fork
is placed in between each pair of adjacent philosophers, and each philosopher may only
use the fork to his left and the fork to his right. However, the philosophers do not speak
to each other.

#### Issues

*[Nota: aquí aparecía una imagen ilustrativa titulada "Illustration of the dining philosophers problem", cuyo contenido visual no se conservó en la extracción del texto.]*

Deadlock would arise if every philosopher held a left fork and waited perpetually for a
right fork ( or vice versa). Originally used as a means of illustrating the problem of
deadlock, this system reaches deadlock when there is a 'cycle of unwarranted requests'.
In this case philosopher P1 waits for the fork grabbed by philosopher P2 who is waiting
for the fork of philosopher P3 and so forth, making a circular chain.
Resource starvation might also occur independently of deadlock if a particular
philosopher is unable to acquire both forks because of a timing problem. For example
there might be a rule that the philosophers put down a fork after waiting five minutes
for the other fork to become available and wait a further five minutes before making
their next attempt. This scheme eliminates the possibility of deadlock ( the system can
always advance to a different state) but still suffers from the problem of livelock. If all
five philosophers appear in the dining room at exactly the same time and each picks up
the left fork at the same time the philosophers will wait five minutes until they all put
their forks down and then wait a further five minutes before they all pick them up again.
Mutual exclusion is the core idea of the problem, and the dining philosophers create a
generic and abstract scenario useful for explaining issues of this type. The failures these
philosophers may experience are analogous to the difficulties that arise in real computer
programming when multiple programs need exclusive access to shared resources. These
issues are studied in the branch of Concurrent Programming. The original problems of
Dijkstra were related to external devices like tape drives. However, the difficulties
studied in the Dining Philosophers problem arise far more often when multiple
processes access sets of data that are being updated. Systems that must deal with a large
number of parallel processes, such as operating system kernels, use thousands of locks
and synchronizations that require strict adherence to methods and protocols if such
problems as deadlock, starvation, or data corruption are to be avoided.

### Solutions

#### Conductor solution

A relatively simple solution is achieved by introducing a waiter at the table.
Philosophers must ask his permission before taking up any forks. Because the waiter is
aware of which forks are in use, he is able to arbitrate and prevent deadlock. When four
of the forks are in use, the next philosopher to request one has to wait for the waiter's
permission, which is not given until a fork has been released. The logic is kept simple
by specifying that philosophers always seek to pick up their left hand fork before their
right hand fork ( or vice versa).
To illustrate how this works, consider the philosophers are labelled clockwise from A to
E. If A and C are eating, four forks are in use. B sits between A and C so has neither
fork available, whereas D and E have one unused fork between them. Suppose D wants
to eat. Were he to take up the fifth fork, deadlock becomes likely. If instead he asks the
waiter and is told to wait, we can be sure that next time two forks are released there will
certainly be at least one philosopher who could successfully request a pair of forks.
Therefore deadlock cannot happen.

#### Resource hierarchy solution

Another simple solution is achieved by assigning a partial order to the resources ( the
forks, in this case), and establishing the convention that all resources will be requested
in order, and released in reverse order, and that no two resources unrelated by order will
ever be used by a single unit of work at the same time. Here, the resources ( forks) will
be numbered 1 through 5, in some order, and each unit of work ( philosopher) will
always pick up the lower-numbered fork first, and then the higher-numbered fork, from
among the two forks he plans to use. Then, he will always put down the higher
numbered fork first, followed by the lower numbered fork. In this case, if four of the
five philosophers simultaneously pick up their lower-numbered fork, only the highest
numbered fork will remain on the table, so the fifth philosopher will not be able to pick
up any fork. Moreover, only one philosopher will have access to that highest-numbered
fork, so he will be able to eat using two forks. When he finishes using the forks, he will
put down the highest-numbered fork first, followed by the lower-numbered fork, freeing
another philosopher to grab the latter and begin eating.
This solution to the problem is the one originally proposed by Dijkstra.
While the resource hierarchy solution avoids deadlocks, it is not always practical,
especially when the list of required resources is not completely known in advance. For
example, if a unit of work holds resources 3 and 5 and then determines it needs resource
2, it must release 5, then 3 before acquiring 2, and then it must re-acquire 3 and 5 in that
order. Computer programs that access large numbers of database records would not run
efficiently if they were required to release all higher-numbered records before accessing
a new record, making the method impractical for that purpose.

#### Monitor solution

The example below shows a solution where the forks are not represented explicitly.
Philosophers can eat if neither of their neighbors are eating. This is comparable to a
system where philosophers that cannot get the second fork must put down the first fork
before they try again.
In the absence of locks associated with the forks, philosophers must ensure that the
decision to begin eating is not based on stale information about the state of the
neighbors. E.g. if philosopher B sees that A is not eating, then turns and looks at C, A
could begin eating while B looks at C. This solution avoids this problem by using a
single mutual exclusion lock. This lock is not associated with the forks but with the
decision procedures that can change the states of the philosophers. This is ensured by
the monitor. The procedures test, pickup and putdown are local to the monitor and share
a mutual exclusion lock. Notice that philosophers wanting to eat do not hold a fork.
When the monitor allows a philosopher who wants to eat to continue, the philosopher
will reacquire the first fork before picking up the now available second fork. When done
eating, the philosopher will signal to the monitor that both forks are now available.
Notice that this example does not tackle the starvation problem. For example,
philosopher B can wait forever if the eating periods of philosophers A and C always
overlap.
To also guarantee that no philosopher starves, one could keep track of the number of
times a hungry philosopher cannot eat when his neighbors put down their forks. If this
number exceeds some limit, the state of the philosopher could change to Starving, and
the decision procedure to pick up forks could be augmented to require that none of the
neighbors are starving.
A philosopher that cannot pick up forks because a neighbor is starving, is effectively
waiting for the neighbor's neighbor to finish eating. This additional dependency reduces
concurrency. Raising the threshold for transition to the Starving state reduces this effect.

#### Chandy / Misra solution

In 1984, K. Mani Chandy and J. Misra proposed a different solution to the dining
philosophers problem to allow for arbitrary agents ( numbered P , ..., P ) to contend for
1 n
an arbitrary number of resources, unlike Dijkstra's solution. It is also completely
distributed and requires no central authority after initialization.
1. For every pair of philosophers contending for a resource, create a fork and give
it to the philosopher with the lower ID. Each fork can either be dirty or clean.
Initially, all forks are dirty.
2. When a philosopher wants to use a set of resources ( i.e. eat), he must obtain the
forks from his contending neighbors. For all such forks he does not have, he
sends a request message.
3. When a philosopher with a fork receives a request message, he keeps the fork if
it is clean, but gives it up when it is dirty. If he sends the fork over, he cleans the
fork before doing so.
4. After a philosopher is done eating, all his forks become dirty. If another
philosopher had previously requested one of the forks, he cleans the fork and
sends it.
This solution also allows for a large degree of concurrency, and will solve an arbitrarily
large problem.
It also solves the starvation problem. The clean / dirty labels act as a way of giving
preference to the most "starved" processes, and a disadvantage to processes that have
just "eaten". One could compare their solution to one where philosophers are not
allowed to eat twice in a row without letting others use the forks in between. Their
solution is more flexible than that, but has an element tending in that direction.
In their analysis they derive a system of preference levels from the distribution of the
forks and their clean/dirty states. They show that this system may describe an acyclic
graph, and if so, the operations in their protocol cannot turn that graph into a cyclic one.
This guarantees that deadlock cannot occur. However, if the system is initialized to a
perfectly symmetric state, like all philosophers holding their left side forks, then the
graph is cyclic at the outset, and their solution cannot prevent a deadlock. Initializing
the system so that philosophers with lower IDs have dirty forks ensure the graph is
initially acyclic.

### Example solution

*[Nota: aquí aparecía una imagen ilustrativa titulada "Solution illustration", cuyo contenido visual no se conservó en la extracción del texto.]*

http://www.shubhammehrotra.co.cc/os/dining.html

Example solution written in Pascal ( using Monitor synchronization)

```pascal

PROGRAM d_p;
CONST
DoomsDay = FALSE;
MONITOR dining_philosophers; // Start of monitor declaration
CONST
Eating = 0;
Hungry = 1;
Thinking = 2;
VAR
i : INTEGER; // init loop variable
state : ARRAY [0..4] OF INTEGER; // Eating, Hungry,
Thinking
can_eat : ARRAY [0..4] OF CONDITION; // one for each
Philosopher
// place for Hungry Ph to wait until forks become available
PROCEDURE test ( k : INTEGER);
BEGIN
IF ( state[k] = Hungry)
AND ( state[( k+4) MOD 5] <> Eating)
AND ( state[( k+1) MOD 5] <> Eating) THEN
BEGIN
state[k] := Eating;
SIGNALC ( can_eat[k]); // End the wait if any
END;
END;
PROCEDURE pickup ( i: INTEGER);
BEGIN
state[i] := Hungry;
WRITELN ('philosopher ',i,' hungry');
test ( i); // are my neighbors eating?
IF state[i] <> Eating THEN
WAITC ( can_eat[i]); // wait until they finish eating
WRITELN ('philosopher ',i,' eating');
END;
PROCEDURE putdown ( i : INTEGER);
BEGIN
state[i] := Thinking;
WRITELN ('philosopher ',i,' thinking');
test ( ( i+4) MOD 5); // give left neighbor chance to eat
test ( ( i+1) MOD 5); // give right neighbor chance to eat
END;
BEGIN // initialize monitor
FOR i := 0 TO 4 DO state[i] := Thinking;
END; // end of monitor definition
PROCEDURE philosopher ( i : INTEGER);
BEGIN
REPEAT
pickup ( i); // pick up forks
putdown ( i); // put down forks
UNTIL DoomsDay;
END;
BEGIN // main program
COBEGIN // start all five processes at once
philosopher ( 0); philosopher ( 1); philosopher ( 2);
philosopher ( 3); philosopher ( 4);
COEND;
END

```

Example Solution written in Java ( using Semaphores)

```java

import java.util.concurrent.Semaphore;
import java.util.Random;
/**
- Five Philosopher problem: How to model limited shared resources
- http://en.wikipedia.org/wiki/Five_philosophers
- This is an update of the original version posted on WikipediA
- JEB 11-04-2010
- /
public class Philosopher extends Thread
{
// Shared by each instance
private static final Random rand = new Random ();
private static int event=0;
// My local stuff
private int id; // Who am I
private Semaphore myFork; // Resource locks
private Semaphore myNeighborsFork;
private int meals = 10; // Max meals
/**
- Constructor: an ID# and two shared resources
- @param i
- @param fork1
- @param fork2
- /
public Philosopher ( int i, Semaphore fork1, Semaphore fork2)
{
id = i;
myFork = fork1;
myNeighborsFork = fork2;
}
/**
- "Lazy" message queue. Original program used a Vector<String>
to
- queue the events and displayed them at the end. I like having
- feedback while the program is running, but the messages are
- sometimes displayed out of order - no biggie.
- @param str
- /
private void postMsg ( String str) {
System.out.printf ("%d %d Philosopher %d %s\n",
System.currentTimeMillis (), ++event, id, str);
}
/**
- Pause - waits a bit ( random fraction of a second)
- /
private void pause ()
{
try
{
sleep ( rand.nextInt ( 1000));
} catch ( InterruptedException e){}
}
/**
- Tell philosopher to think - he waits a bit
- /
private void think ()
{
postMsg ("is thinking");
pause ();
}
/**
- Tell philosopher to eat. Tries to acquire resources ( forks)
- Possible modification: Doesn't change a state
- ( hungry, starving, etc.) if they can't get a fork
- Possible modification: could return a boolean indicating
success
- /
private void trytoeat ()
{
postMsg ("is hungry and is trying to pick up his forks");
pause ();
try {
// Semaphore - waits on his own fork if necessary
myFork.acquire ();
// He's picked up his own fork, now try and grab his
neighbor's fork
// ( does not wait)
if (!myNeighborsFork.tryAcquire ()) {
// Unsuccessful, guess he's fasting today
postMsg (">>>> was not able to get his neighbor's
fork");
return;
};
// Success! begins to eat
postMsg ("picked up his forks and is eating meal #" + ( 10 -
--meals));
pause ();
// Now put down the forks
postMsg ("puts down his forks");
myNeighborsFork.release ();
} catch ( InterruptedException e) {
// In case the thread is interrupted
postMsg ("was interrupted while waiting for his fork");
}
finally { // always puts his own fork back down
myFork.release ();
}
}
/**
- philosophise until all meals are consumed
- /
@Override
public void run ()
{
while ( meals > 0)
{
think ();
trytoeat ();
}
}
/**
- Main program
- Create resources ( forks) as semaphores
- create philosophers
- start philosophers
- wait for completion
- /
// Main program
public static void main ( String[] args)
{
System.out.println ("Begin");
final int N = 5; // five philosophers, five forks
// Create the forks, 1 fork per philosopher
Semaphore[] fork = new Semaphore[N];
for ( int f = 0; f < N; f++) {
// each fork is a single resource
fork[f] = new Semaphore ( 1, true);
}
// Create the philosophers, pass in their forks
Philosopher[] philosopher = new Philosopher[N];
for ( int me = 0; me < N; me++) {
// determine my right-hand neighbor's ID
int myneighbor = me + 1;
if ( myneighbor == N) myneighbor = 0;
// Initialize each philosopher ( no pun intended)
philosopher[me] = new Philosopher ( me, fork[me],
fork[myneighbor]); // :)
}
// Start the philosophers
for ( int i = 0; i < N; i++) {
philosopher[i].start ();
}
// Wait for them to finish
for ( int i = 0; i < N; i++) {
try {
philosopher[i].join ();
} catch ( InterruptedException ex) { }
}
// All done
System.out.println ("Done");
}
}

```

### See also

 Cigarette smokers problem
 Producers-consumers problem
 Readers-writers problem
 Sleeping barber problem

### References

1. ^ J. Díaz; I. Ramos ( 1981). Formalization of Programming Concepts:
International Colloquium, Peniscola, Spain, April 19–25, 1981. Proceedings.
Birkhäuser. pp. 323 , 326. ISBN 9783540106999.
http://books.google.com/books?id=pl4VJKQlcG4C.
2. ^ Hoare, C. A. R. ( 2004). "Communicating Sequential Processes". usingcsp.com
( originally published in 1985 by Prentice Hall International).
http://www.usingcsp.com/cspbook.pdf.
 Silberschatz, Abraham; Peterson, James L. ( 1988). Operating Systems Concepts.
Addison-Wesley. ISBN 0-201-18760-4.
 Chandy, K.M.; Misra, J. ( 1984). The Drinking Philosophers Problem. ACM
Transactions on Programming Languages and Systems.
 Dijkstra, E. W. ( 1971, June). Hierarchical ordering of sequential processes. Acta
Informatica 1 ( 2): 115–138.
 Lehmann, D. J., Rabin M. O, ( 1981). On the Advantages of Free Choice: A
Symmetric and Fully Distributed Solution to the Dining Philosophers Problem.
Principles Of Programming Languages 1981 ( POPL'81), pp. 133–138.

### External links

 Illustration of the dining philosophers problem ( Java applet)
 Discussion of the problem with solution code for 2 or 4 philosophers
 Discussion of various solutions 1
 Discussion of various solutions 2
 Discussion of a solution using continuation based threads ( cbthreads)
 Distributed symmetric solutions
 Programming the Dining Philosophers with Simulation
 Interactive example of the Philosophers problem ( Java required)
 Satan Comes to Dinner
 Wot No Chickens? - Peter H. Welch proposed the Starving Philosophers variant
that demonstrates an unfortunate consequence of the behaviour of Java thread
monitors is to make thread starvation more likely than strictly necessary.
 ThreadMentor
 Solving The Dining Philosophers Problem With Asynchronous Agents

## Deadlock

A deadlock is a situation where in two or more competing actions are each waiting for
the other to finish, and thus neither ever does. It is often seen in a paradox like the
"chicken or the egg". The concept of a Catch 22 is similar.
When two trains approach each other at a crossing, both shall come to a full
“ ”
stop and neither shall start up again until the other has gone.
— Statute passed by the Kansas Legislature[1]
In computer science, Coffman deadlock refers to a specific condition when two or
more processes are each waiting for each other to release a resource, or more than two
processes are waiting for resources in a circular chain ( see Necessary conditions).
Deadlock is a common problem in multiprocessing where many processes share a
specific type of mutually exclusive resource known as a software lock or soft lock.
Computers intended for the time-sharing and/or real-time markets are often equipped
with a hardware lock ( or hard lock) which guarantees exclusive access to processes,
forcing serialized access. Deadlocks are particularly troubling because there is no
general solution to avoid ( soft) deadlocks.
This situation may be likened to two people who are drawing diagrams, with only one
pencil and one ruler between them. If one person takes the pencil and the other takes the
ruler, a deadlock occurs when the person with the pencil needs the ruler and the person
with the ruler needs the pencil to finish his work with the ruler. Neither request can be
satisfied, so a deadlock occurs.
The telecommunications description of deadlock is weaker than Coffman deadlock
because processes can wait for messages instead of resources. A deadlock can be the
result of corrupted messages or signals rather than merely waiting for resources. For
example, a dataflow element that has been directed to receive input on the wrong link
will never proceed even though that link is not involved in a Coffman cycle.
Contents [hide]

- 1 Examples
  - 1.1 Necessary conditions
  - 1.2 Prevention
  - 1.3 Avoidance
  - 1.4 Detection
- 2 Distributed deadlock
  - 2.1 Distributed deadlock prevention
- 3 Livelock
- 4 See also
- 5 References
- 6 Further reading
- 7 External links

### Examples

An example of a deadlock which may occur in database products is the following.
Client applications using the database may require exclusive access to a table, and in
order to gain exclusive access they ask for a lock. If one client application holds a lock
on a table and attempts to obtain the lock on a second table that is already held by a
second client application, this may lead to deadlock if the second application then
attempts to obtain the lock that is held by the first application. ( But this particular type
of deadlock is easily prevented, e.g., by using an all-or-none resource allocation
algorithm.)
Another example might be a text formatting program that accepts text sent to it to be
processed and then returns the results, but does so only after receiving "enough" text to
work on ( e.g. 1KB). A text editor program is written that sends the formatter some text
and then waits for the results. In this case a deadlock may occur on the last block of
text. Since the formatter may not have sufficient text for processing, it will suspend
itself while waiting for the additional text, which will never arrive since the text editor
has sent it all of the text it has. Meanwhile, the text editor is itself suspended waiting for
the last output from the formatter. This type of deadlock is sometimes referred to as a
deadly embrace ( properly used only when only two applications are involved) or
starvation. However, this situation, too, is easily prevented by having the text editor
send a forcing message ( e.g. EOF, ( End Of File)) with its last ( partial) block of text,
which will force the formatter to return the last ( partial) block after formatting, and not
wait for additional text.
In communications, corrupted messages may cause computers to go into bad states
where they are not communicating properly. The network may be said to be deadlocked
even though no computer is waiting for a resource. This is different than a Coffman
deadlock.

#### Necessary conditions

There are four necessary and sufficient conditions for a Coffman deadlock to occur,
known as the Coffman conditions from their first description in a 1971 article by
Edward G. Coffman, Jr..
1. Mutual exclusion condition: a resource that cannot be used by more than one
process at a time
2. Hold and wait condition: processes already holding resources may request new
resources held by other processes
3. No preemption condition: No resource can be forcibly removed from a process
holding it, resources can be released only by the explicit action of the process.
The first three conditions are necessary but not sufficient for a deadlock to exist. For
deadlock to actually take place, a fourth condition is required:
1. Circular wait condition: two or more processes form a circular chain where each
process waits for a resource that the next process in the chain holds. When
circular waiting is triggered by mutual exclusion operations it is sometimes
called lock inversion.[2]

#### Prevention

 Removing the mutual exclusion condition means that no process may have
exclusive access to a resource. This proves impossible for resources that cannot
be spooled, and even with spooled resources deadlock could still occur.
Algorithms that avoid mutual exclusion are called non-blocking synchronization
algorithms.
 The "hold and wait" conditions may be removed by requiring processes to
request all the resources they will need before starting up ( or before embarking
upon a particular set of operations); this advance knowledge is frequently
difficult to satisfy and, in any case, is an inefficient use of resources. Another
way is to require processes to release all their resources before requesting all the
resources they will need. This too is often impractical. ( Such algorithms, such as
serializing tokens, are known as the all-or-none algorithms.)
 A "no preemption" ( lockout) condition may also be difficult or impossible to
avoid as a process has to be able to have a resource for a certain amount of time,
or the processing outcome may be inconsistent or thrashing may occur.
However, inability to enforce preemption may interfere with a priority
algorithm. ( Note: Preemption of a "locked out" resource generally implies a
rollback, and is to be avoided, since it is very costly in overhead.) Algorithms
that allow preemption include lock-free and wait-free algorithms and optimistic
concurrency control.
 The circular wait condition: Algorithms that avoid circular waits include
"disable interrupts during critical sections", and "use a hierarchy to determine a
partial ordering of resources" ( where no obvious hierarchy exists, even the
memory address of resources has been used to determine ordering) and
Dijkstra's solution.

#### Avoidance

Deadlock can be avoided if certain information about processes is available in advance
of resource allocation. For every resource request, the system sees if granting the
request will mean that the system will enter an unsafe state, meaning a state that could
result in deadlock. The system then only grants requests that will lead to safe states. In
order for the system to be able to figure out whether the next state will be safe or unsafe,
it must know in advance at any time the number and type of all resources in existence,
available, and requested. One known algorithm that is used for deadlock avoidance is
the Banker's algorithm, which requires resource usage limit to be known in advance.
However, for many systems it is impossible to know in advance what every process will
request. This means that deadlock avoidance is often impossible.
Two other algorithms are Wait/Die and Wound/Wait, each of which uses a symmetry-
breaking technique. In both these algorithms there exists an older process ( O) and a
younger process ( Y). Process age can be determined by a timestamp at process creation
time. Smaller time stamps are older processes, while larger timestamps represent
younger processes.
Wait/Die Wound/Wait
O needs a resource held by Y O waits Y dies
Y needs a resource held by O Y dies Y waits
It is important to note that a process may be in an unsafe state but would not result in a
deadlock. The notion of safe/unsafe states only refers to the ability of the system to
enter a deadlock state or not. For example, if a process requests A which would result in
an unsafe state, but releases B which would prevent circular wait, then the state is
unsafe but the system is not in deadlock.

#### Detection

Often, neither avoidance nor deadlock prevention may be used. Instead deadlock
detection and process restart are used by employing an algorithm that tracks resource
allocation and process states, and rolls back and restarts one or more of the processes in
order to remove the deadlock. Detecting a deadlock that has already occurred is easily
possible since the resources that each process has locked and/or currently requested are
known to the resource scheduler or OS.
Detecting the possibility of a deadlock before it occurs is much more difficult and is, in
fact, generally undecidable, because the halting problem can be rephrased as a deadlock
scenario. However, in specific environments, using specific means of locking resources,
deadlock detection may be decidable. In the general case, it is not possible to
distinguish between algorithms that are merely waiting for a very unlikely set of
circumstances to occur and algorithms that will never finish because of deadlock.
Deadlock detection techniques include, but is not limited to, Model checking. This
approach constructs a Finite State-model on which it performs a progress analysis and
finds all possible terminal sets in the model. These then each represent a deadlock.

### Distributed deadlock

This article's tone or style may not be appropriate for Wikipedia. Specific
concerns may be found on the talk page. See Wikipedia's guide to writing better
articles for suggestions. ( November 2010)
Distributed deadlocks can occur in distributed systems when distributed transactions or
concurrency control is being used. Distributed deadlocks can be detected either by
constructing a global wait-for graph, from local wait-for graphs at a deadlock detector
or by a distributed algorithm like edge chasing.
In a Commitment ordering based distributed environment ( including the Strong strict
two-phase locking ( SS2PL, or rigorous) special case) distributed deadlocks are resolved
automatically by the atomic commitment protocol ( e.g. two-phase commit ( 2PC)), and
no global wait-for graph or other resolution mechanism are needed. Similar automatic
global deadlock resolution occurs also in environments that employ 2PL that is not
SS2PL ( and typically not CO; see Deadlocks in 2PL). However 2PL that is not SS2PL
is rarely utilized in practice.
Phantom deadlocks are deadlocks that are detected in a distributed system due to system
internal delays, but no longer actually exist at the time of detection.

#### Distributed deadlock prevention

Lets consider the "When two trains approach each other at a crossing" example defined
above. Just-in-time Prevention works like having a person standing at the crossing ( the
crossing guard) with a switch that will let only one train onto "super tracks" which runs
above and over the other waiting train ( s).
Before we look into threads using Just-in-time Prevention, lets look into the conditions
which already exist for regular locking.
 For non-recursive locks, this lock may be entered only once ( where a single
thread entering twice without unlocking will cause a deadlock, or throw an
exception to enforce circular wait prevention).
 For recursive locks, only one thread is allowed to pass through a lock. If any
other threads enter the lock, they must wait until the initial thread that passed
through completes n number of times it has entered.
So the issue with the first one is it does no deadlock prevention at all. The second
doesn't do Distributed deadlock prevention. But the 2nd one is redefined to prevent a
deadlock scenario the first one doesn't address. And the only other scenario I am aware
of that may cause deadlocks is when two or more lockers lock on each other. So why
not expand the definition above one more time?
Well, we can, if we use add a variable to the recursive lock condition which guarantees
that at least one thread runs among all locks—distributed deadlock prevention. And just
like having a super track in the train example, I use "super thread" in this locking
example.
 Recursively, only one thread is allowed to pass through a lock. If other threads
enter the lock, they must wait until the initial thread that passed through
completes n number of times. But if the number of threads that enter locking
equal the number that are locked, assign one thread as the super-thread, and only
allow it to run ( tracking the number of times it enters/exits locking) until it
completes.
After a super-thread is finished, the condition changes back to using the logic from the
recursive lock, and the exiting super-thread
1. sets itself as not being a super-thread
2. notifies the locker that other locked, waiting threads need to re-check this
condition
If a deadlock scenario exists, set a new super-thread and follow that logic. Otherwise,
resume regular locking.

##### Issues not addressed above

A lot of confusion revolves around the halting problem. But this logic in-no-way solves
the halting problem. This is because we know and control the conditions in which
locking occurs, giving us a specific solution ( instead of the otherwise required general
solution the halting problem requires). Still this locker prevents all deadlocked!
Well, it does when only considering locks using this logic. But if it is use with other
locking mechanisms, a lock that is started never unlocks ( e.g. exception thrown jumping
out without unlocking, looping indefinitely within a lock, or coding error forgetting to
call unlock), deadlocking is very much possible. And to increase our condition to
include these would require solving the halting issue, since we would be dealing with
conditions we know nothing about and are unable to change.

Another issue is that this doesn't address the temporary deadlocking issue ( not really a
deadlock, but a performance killer), where two or more threads lock on each other while
another unrelated threads is running. These temporary deadlocks could have a thread
running exclusively within them, increasing parallelism. But because of how the
distributed deadlock detection works for all locks, and not subsets therein, the unrelated
running thread must complete before performing the super-thread logic to remove the
temporary deadlock.
I hope you see the temporary live-lock scenario in the above. If another unrelated
running thread begins before the first unrelated thread exits, another duration of
temporary deadlocking will occur. And if this happens continuously ( extremely rare),
the temporary deadlock can be extended until right before the program exits, when the
other unrelated threads are guaranteed to finish ( because of the guarantee that one
thread will always run to completion).

##### Further expansion

This can be further expanded to involve additional logic to increase parallelism where
temporary deadlocks might otherwise occur. But for each step of adding more logic, we
add more overhead.

A couple of examples include: expanding distributed super-thread locking mechanism
to consider each subset of existing locks; Wait-For-Graph ( WFG) [1] algorithms, which
tracks all cycles that cause deadlocks ( including temporary deadlocks); and heuristics
algorithms which don't necessarily increase parallelism in 100% of the places that
temporary deadlocks are possible, but instead compromise by solving them in enough
places that performance/overhead vs parallelism is acceptable ( e.g. for each processor
available, work towards finding deadlock cycles less than the number of processors + 1
deep).

### Livelock

A livelock is similar to a deadlock, except that the states of the processes involved in
the livelock constantly change with regard to one another, none progressing.[3] Livelock
is a special case of resource starvation; the general definition only states that a specific
process is not progressing.[4]
A real-world example of livelock occurs when two people meet in a narrow corridor,
and each tries to be polite by moving aside to let the other pass, but they end up swaying
from side to side without making any progress because they both repeatedly move the
same way at the same time.

Livelock is a risk with some algorithms that detect and recover from deadlock. If more
than one process takes action, the deadlock detection algorithm can be repeatedly
triggered. This can be avoided by ensuring that only one process ( chosen randomly or
by priority) takes action.[5]

### See also

- Banker's algorithm - Linearizability
- Catch 22 - Model checker can be used to
- Deadlock provision - formally verify that a system will
- Dining philosophers problem - never enter a deadlock.
- File locking - Ostrich algorithm
- Gridlock ( in vehicular traffic) - Priority inversion
- Hang - Race condition
- Impasse - Sleeping barber problem
- Infinite loop - Stalemate
 Readers-writer lock
 Synchronization

### References

1. ^ A Treasury of Railroad Folklore, B.A. Botkin & A.F. Harlow, p. 381
2. ^ Silviu Andrica, Cristian Zamfir, George Candea. "GoodRun: Enforcing Good
Runs in Parallel Programs". EuroSys 2009.
https://dslabpc10.epfl.ch/ssl_read/zamfir/goodrun_wip_eurosys09.pdf.
3. ^ Mogul, Jeffrey C.; K. K. Ramakrishnan ( 1996). "Eliminating receive livelock
in an interrupt-driven kernel". http://citeseer.ist.psu.edu/326777.html.
4. ^ Anderson, James H.; Yong-jik Kim ( 2001). "Shared-memory mutual
exclusion: Major research trends since 1986".
http://citeseer.ist.psu.edu/anderson01sharedmemory.html.
5. ^ Zöbel, Dieter ( October 1983). "The Deadlock problem: a classifying
bibliography". ACM SIGOPS Operating Systems Review 17 ( 4): 6–15.
ISSN 0163-5980. http://doi.acm.org/10.1145/850752.850753.

### Further reading

 Kaveh, Nima; Emmerich, Wolfgang. Deadlock Detection in Distributed Object
Systems. London: University College London.
http://www.cs.ucl.ac.uk/staff/w.emmerich/publications/ESEC01/ModelChecking
/esec.pdf.
 Bensalem, Saddek; Fernandez, Jean-Claude; Havelund, Klaus; Mounier, Laurent
( 2006). "Confirmation of deadlock potentials detected by runtime analysis".
Proceedings of the 2006 workshop on Parallel and distributed systems: Testing
and debugging ( ACM): 41–50. doi:10.1145/1147403.1147412.
 Coffman, Edward G., Jr.; Elphick, Michael J.; Shoshani, Arie ( 1971). "System
Deadlocks". ACM Computing Surveys 3 ( 2): 67–78.
doi:10.1145/356586.356588.
http://www.cs.umass.edu/~mcorner/courses/691J/papers/TS/coffman_deadlocks/
coffman_deadlocks.pdf.
 Mogul, Jeffrey C.; Ramakrishnan, K. K. ( 1997). "Eliminating receive livelock in
an interrupt-driven kernel". ACM Transactions on Computer Systems 15 ( 3):
217–252. doi:10.1145/263326.263335. ISSN 07342071.
 Havender, James W. ( 1968). "Avoiding deadlock in multitasking systems". IBM
Systems Journal 7 ( 2): 74.
http://domino.research.ibm.com/tchjr/journalindex.nsf/a3807c5b4823c53f85256
561006324be/c014b699abf7b9ea85256bfa00685a38?OpenDocument.
 Holliday, JoAnne L.; El Abbadi, Amr. "Distributed Deadlock Detection".
Encyclopedia of Distributed Computing ( Kluwer Academic Publishers).
http://www.cse.scu.edu/~jholliday/dd_9_16.htm.
 Knapp, Edgar ( 1987). "Deadlock detection in distributed databases". ACM
Computing Surveys 19 ( 4): 303–328. doi:10.1145/45075.46163.
ISSN 03600300.

### External links

 "Advanced Synchronization in Java Threads" by Scott Oaks and Henry Wong
 Deadlock Detection Agents
 DeadLock at the Portland Pattern Repository
 Etymology of "Deadlock"
 ARCS - A Web Service approach to alleviating deadlock
 Non-Hard Locking Read-Write Locker
Read more: http://www.answers.com/topic/deadlock#ixzz1FdPcSZID
