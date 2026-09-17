Based on your instructions, here is the organized, focused, and code-minimized summary of your notes for technical round preparation.

# Section 3 (Core Utilities) -> Multi-Threading & Concurrency

- Thread vs. Process:

- A thread is a lightweight sub-process (e.g., screen share, chat box). Multiple threads run concurrently and can communicate with each other.
- A process is a collection of threads (e.g., Zoom Meeting). Multiple processes run concurrently but are independent and cannot communicate with each other.

- Multitasking: Executing several tasks simultaneously.

- Thread-based: Tasks are part of the same program; best suited for the programmatic level.
- Process-based: Tasks are independent processes; best suited for the OS level.

- Multi-Threading Basics: Executing several threads simultaneously to implement multimedia graphics, video games, and animations. In Java, the API handles 90% of the multithreading work.
- Ways to Create a Thread:

- Extending the Thread class.
- Implementing the Runnable interface.

- Thread Execution & Schedulers:

- Thread Scheduler: Decides execution order when multiple threads wait. The mechanism depends on the JVM vendor, meaning execution order or exact output cannot be expected.
- t.start() vs t.run(): Calling start() creates a new thread that executes run() automatically. Calling run() directly does not create a thread and executes like a normal method.

- Thread Lifecycle State: Born/New -> Ready/Runnable (after start()) -> Running (when allocated CPU) -> Dead (when run() completes).
- Thread Names & Priorities:

- Threads have explicitly provided or JVM-generated names (e.g., setName(), getName()).
- Priority ranges from 1 (MIN_PRIORITY) to 10 (MAX_PRIORITY), with 5 as NORM_PRIORITY. Exceeding 10 throws an IllegalArgumentException.
- Highest priority threads execute first; execution order for same-priority threads is unpredictable.

- Daemon Thread: A low-priority background thread (like Garbage Collector) providing services to user threads. It dies automatically when all user threads die.
- Preventing Execution:

- yield(): Pauses the current thread to give a chance to other waiting threads of the same priority.
- join(): Makes a thread wait until the completion of another specific thread; throws InterruptedException.
- sleep(): Pauses a thread for a specific duration; throws InterruptedException.

- Synchronization:

- Addresses data inconsistency and thread interference by allowing only one thread to execute at a time using a lock mechanism.
- Applicable to methods and blocks.
- Provides thread safety but increases thread waiting time, affecting performance.
- Static Synchronization: The lock is placed on the class rather than the object.

- Inter-Thread Communication:

- Achieved via wait(), notify(), and notifyAll() methods present in the Object class.
- Requires a synchronized area. wait() immediately releases the lock, while notify()/notifyAll() do not.

- Deadlocks: Occurs when two threads are mutually waiting for an object lock acquired by the other, and neither is able to release their lock.
