- [Что такое ОС](Что%20такое%20ОС.md)
- [История операционных систем](История%20операционных%20систем.md)
- [Обзор компьютерного оборудования](Обзор%20компьютерного%20оборудования.md)
- [Зоопарк операционных систем](Зоопарк%20операционных%20систем.md)
- [Концепции операционных систем](Концепции%20операционных%20систем.md)
- [Системные вызовы](Системные%20вызовы.md)
- [Структура ОС](Структура%20ОС.md)
- [Мир согласно С](Мир%20согласно%20С.md)

PROBLEMS
1. What are the two main functions of an operating system?

An operating system must provide the users with an extended machine, and it must manage the I/O devices and other system resources. To some extent, these are different functions.

2. What is multiprogramming?

Multiprogramming is the technique of keeping **multiple processes in memory at the same time** and switching the CPU among them. The main goal is to **maximize CPU utilization** by ensuring the CPU is never idle while some process is waiting for I/O operations to complete.

3. In Sec. 1.4, nine different types of operating systems are described. Give a list of possible applications for each of these systems (at least one for each of the operating systems types).
   
• Mainframe operating system: Sales reporting for a chain of stores.
• Server operating system: Speech-to-text conversion service for intelligent assistant Alice.
• Multiprocessor operating system: Video editing and rendering.
• Personal computer operating system: Word processing application.
• Handheld computer operating system: PDA (Personal Digital Assistant) that can be held in your hand during operation.
• Embedded operating system: Programming a DVD recorder for recording TV.
• Sensor-node operating system: Glean information about enemy movements on battleϐields.
• Real-time operating system: Air trafϐic control system.
• Smart-card operating system: Electronic payment

4. To use cache memory, main memory is divided into cache lines, typically 32 or 64 bytes long. An entire cache line is cached at once. What is the advantage of caching an entire line instead of a single byte or word at a time?

Empirical evidence shows that memory access exhibits the principle of locality of reference, where if one location is read then the probability of accessing nearby locations next is very high, particularly the following memory locations. So, by caching an entire cache line, the probability of a cache hit next is increased. Also, modern hardware can do a block transfer of 32 or 64 bytes into a cache line much faster than reading the same data as individual words

5. What is spooling? Do you think that advanced personal computers will have spooling as a standard feature in the future?

Input spooling is the technique of reading in jobs, for example, from cards, onto the disk, so that when the currently executing processes are finished, there will be work waiting for the CPU. Output spooling consists of first copying printable files to disk before printing them, rather than printing directly as the output is generated. Input spooling on a personal computer is not very likely, but output spooling is.

5. On early computers, every byte of data read or written was handled by the CPU (i.e., there was no DMA). What implications does this have for multiprogramming?

The prime reason for multiprogramming is to give the CPU something to do while waiting for I/O to complete. If there is no DMA, the CPU is fully occupied doing I/O, so there is nothing to be gained (at least in terms of CPU utilization) by multiprogramming. No matter how much I/O a program does, the CPU will be 100% busy. This of course assumes the major delay is the wait
while data are copied. A CPU could do other work if the I/O were slow for other reasons (arriving on a serial line, for instance).

6. Why was timesharing not widespread on second-generation computers?

Second-generation computers did not have the necessary hardware to protect the operating system from malicious user programs.

7. Instructions related to accessing I/O devices are typically privileged instructions, that is, they can be executed in kernel mode but not in user mode. Give a reason why these instructions are privileged.

Access to I/O devices (e.g., a printer) is typically restricted for different users. Some users may be allowed to print as many pages as they like, some users may not be allowed to print at all, while some users may be limited to printing only a certain number of pages. These restrictions are set by system administrators based on some policies. Such policies need to be enforced so that user-level programs cannot interfere with them.

These instructions are privileged to prevent user programs from directly accessing hardware devices. This is necessary to effectively manage resources and prevent conflicts or errors that could disrupt the entire system.

8. One reason GUIs were initially slow to be adopted was the cost of the hardware needed to support them. How much video RAM is needed to support a 25-line × 80-row character monochrome text screen? How much for a 1024 × 768-pixel 24-bit color bitmap? What was the cost of this RAM at 1980 prices ($5/KB)? How much is it now?

A 25 $\times$ 80 character monochrome text screen requires a 2000-byte buffer. The 1200 $\times$ 900 pixel 24-bit color bitmap requires 3,240,000 bytes. In 1980 these two options would have cost $10 and $15,820, respectively. For current prices, check on how much RAM currently costs, probably pennies per MB.

9. There are several design goals in building an operating system, for example, resource utilization, timeliness, robustness, and so on. Give an example of two design goals that may contradict one another.

Maximum performance (efficient use of resources) and high reliability. Optimizing for maximum speed can lead to less error checking and, as a result, reduced reliability.

Consider fairness and real time. Fairness requires that each process be allocated its resources in a fair way, with no process getting more than its fair share. On the other hand, real time requires that resources be allocated based on the times when different processes must complete their execution. A real time process may get a disproportionate share of the resources.

10. What is the difference between kernel and user mode? Explain how having two distinct modes aids in designing an operating system.

Most modern CPUs provide two modes of execution: kernel mode and user mode. The CPU can execute every instruction in its instruction set and use every feature of the hardware when executing in kernel mode. However, it can execute only a subset of instructions and use only subset of features when executing in the user mode. Having two modes allows designers to run user programs in user mode and thus deny them access to critical instructions.

11. A 255-GB disk has 65,536 cylinders with 255 sectors per track and 512 bytes per sector. How many platters and heads does this disk have? Assuming an average cylinder seek time of 11 msec, average rotational delay of 7 msec. and reading rate of 100 MB/sec, calculate the average time it will take to read 100 KB from one sector.

Number of heads = 255 GB / (65,536 $\times$ 255 $\times$ 512) B = 32
Number of platters = 32/2 = 16
The time for a read operation to complete is seek time + rotational latency + transfer time. The seek time is 11 ms, the rotational latency is 7 ms and the transfer time is 1 ms, so the average transfer takes 19 ms.

12. Consider a system that has two CPUs, each CPU having two threads (hyperthreading). Suppose three programs, P0, P1, and P2, are started with run times of 5, 10 and 20 msec, respectively. How long will it take to complete the execution of these programs? Assume that all three programs are 100% CPU bound, do not block during execution, and do not change CPUs once assigned.

It may take 20, 25 or 30 msec to complete the execution of these programs depending on how the operating system schedules them. If P0 and P1 are scheduled on the same CPU and P2 is scheduled on the other CPU, it will take 20 msec. If P0 and P2 are scheduled on the same CPU and P1 is scheduled on the other CPU, it will take 25 msec. If P1 and P2 are scheduled on the same CPU and P0 is scheduled on the other CPU, it will take 30 msec. If all three are on the same CPU, it will take 35 msec.

13. List some differences between personal computer operating systems and mainframe operating systems.

Personal computer systems are always interactive, often with only a single user. Mainframe systems nearly always emphasize batch or timesharing with many users. Protection is much more of an issue on mainframe systems, as is efficient use of all resources.

14. A computer has a pipeline with four stages. Each stage takes the same time to do its work, namely, 1 nsec. How many instructions per second can this machine execute?

Every nanosecond one instruction emerges from the pipeline. This means the machine is executing 1 billion instructions per second. It does not matter at all how many stages the pipeline has. A 10-stage pipeline with 1 ns per stage would also execute 1 billion instructions per second. All that matters is how often a finished instruction pops out the end of the pipeline.

15. Consider a computer system that has cache memory, main memory (RAM) and disk, and an operating system that uses virtual memory. It takes 2 nsec to access a word from the cache, 10 nsec to access a word from the RAM, and 10 msec to access a word from the disk. If the cache hit rate is 95% and main memory hit rate (after a cache miss) is 99%, what is the average time to access a word?

0.95 × 2 nsec (word is in the cache) + 0.05 ×0.99 ×10 nsec (word is in RAM, but not in the cache)+ 0.05 ×0.01 ×10,000,000 nsec (word on disk only)= 5002.395 nsec= 5.002395µsec

16. When a user program makes a system call to read or write a disk file, it provides an indication of which file it wants, a pointer to the data buffer, and the count. Control is then transferred to the operating system, which calls the appropriate driver. Suppose that the driver starts the disk and terminates until an interrupt occurs. In the case of reading from the disk, obviously the caller will have to be blocked (because there are no data for it). What about the case of writing to the disk? Need the caller be blocked awaiting completion of the disk transfer?

Maybe. If the caller gets control back and immediately overwrites the data, when the write finally occurs, the wrong data will be written. However, if the driver first copies the data to a private buffer before returning, then the caller can be allowed to continue immediately. Another possibility is to allow the caller to continue and give it a signal when the buffer may be reused, but this is tricky and error prone.

17. What is the key difference between a trap and an interrupt?

A trap is caused by the program and is synchronous with it. If the program is run again and again, the trap will always occur at exactly the same position in the instruction stream. An interrupt is caused by an external event and its timing is not reproducible.

18. Is there any reason why you might want to mount a file system on a nonempty directory? If so, what is it?

Mounting a Þle system makes any Þles already in the mount-point directory inaccessible, so mount points are normally empty. Howev er, a system administrator might want to copy some of the most important Þles normally located in the mounted directory to the mount point so they could be found in their normal path in an emergency when the mounted device was being repaired.

19. What is the purpose of a system call in an operating system?

A system call allows a user process to access and execute operating system functions inside the kernel. User programs use system calls to invoke operating system services.

20. Give one reason why mounting file systems is a better design option than prefixing path names with a drive name or number. Explain why file systems are almost always mounted on empty directories.

PreÞxing path names with a drive name or number makes the Þle system de-

vice dependent. If the directory on which a new Þle system is mounted con-

tained any Þles or subdirectories, those Þles or subdirectories would not be accessible while the administrator tries to Þnd the backup tape.

21. For each of the following system calls, give a condition that causes it to fail: open, close, and lseek.
22. What type of multiplexing (time, space, or both) can be used for sharing the following resources: CPU, memory, SSD/disk, network card, printer, keyboard, and display?
23. Can the 
    `{C} count = write(fd, buffer, nbytes);` 
    call return any value in count other than nbytes? If so, why?
24. A file whose file descriptor is fd contains the following sequence of bytes: 2, 7, 1, 8, 2, 8, 1, 8, 2, 8, 4. The following system calls are made: 
    `{C}lseek(fd, 3, SEEK SET);` 
    `{c}read(fd, &buffer, 4);`
    where the lseek call makes a seek to byte 3 of the file. What does buffer contain after the read has completed?


25. Suppose that a 10-MB file is stored on a disk on the same track (track 50) in consecutive sectors. The disk arm is currently situated over track number 100. How long will it take to retrieve this file from the disk? Assume that it takes about 1 msec to move the arm from one cylinder to the next and about 5 msec for the sector where the beginning of the file is stored to rotate under the head. Also, assume that reading occurs at a rate of 100 MB/s.
26. What is the essential difference between a block special file and a character special file?
27. In the example given in Fig. 1-17, the library procedure is called read and the system call itself is called read. Is it essential that both of these have the same name? If not, which one is more important?
28. The client-server model is popular in distributed systems. Can it also be used in a single-computer system?
29. To a programmer, a system call looks like any other call to a library procedure. Is it important that a programmer know which library procedures result in system calls? Under what circumstances and why?
30. Figure 1-23 shows that a number of UNIX system calls have no Win32 API equivalents. For each of the calls listed as having no Win32 equivalent, what are the consequences for a programmer of converting a UNIX program to run under Windows?
31. A portable operating system is one that can be ported from one system architecture to another without any modification. Explain why it is infeasible to build an operating system that is completely portable. Describe two high-level layers that you will have in designing an operating system that is highly portable.
32. Explain how separation of policy and mechanism aids in building microkernel-based operating systems.
33. Virtual machines have become very popular for a variety of reasons. Nevertheless, they have some downsides. Name one.
34. Here are some questions for practicing unit conversions: 
    (a) How long is a microyear in seconds?
	(b) Micrometers are often called microns. How long is a gigamicron?
	(c) How many bytes are there in a 1-TB memory?
	(d) The mass of the earth is 6000 yottagrams. What is that in grams?
35. Write a shell that is similar to Fig. 1-19 but contains enough code that it actually works so you can test it. You might also add some features such as redirection of input and output, pipes, and background jobs.
36. If you have a personal UNIX-like system (Linux, MINIX 3, FreeBSD, etc.) available that you can safely crash and reboot, write a shell script that attempts to create an unlimited number of child processes and observe what happens. Before running the experiment, type sync to the shell to flush the file system buffers to disk to avoid ruining the file system. You can also do the experiment safely in a virtual machine. Note: Do not try this on a shared system without first getting permission from the system administrator. The consequences will be instantly obvious so you are likely to be caught and sanctions may follow.
37. Examine and try to interpret the contents of a UNIX-like or Windows directory with a tool like the UNIX od program. (Hint: How you do this will depend upon what the OS allows. One trick that may work is to create a directory on a USB stick with one operating system and then read the raw device data using a different operating system that allows such access.)