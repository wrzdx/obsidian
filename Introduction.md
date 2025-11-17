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

5. What is spooling? Do you think that advanced personal computers will have spooling
as a standard feature in the future?
6. On early computers, every byte of data read or written was handled by the CPU (i.e.,
there was no DMA). What implications does this have for multiprogramming?
7. Why was timesharing not widespread on second-generation computers?
8. Instructions related to accessing I/O devices are typically privileged instructions, that
is, they can be executed in kernel mode but not in user mode. Give a reason why these
instructions are privileged.
9. One reason GUIs were initially slow to be adopted was the cost of the hardware need-
ed to support them. How much video RAM is needed to support a 25-line × 80-row
character monochrome text screen? How much for a 1024 × 768-pixel 24-bit color bit-
map? What was the cost of this RAM at 1980 prices ($5/KB)? How much is it now?
10. There are several design goals in building an operating system, for example, resource
utilization, timeliness, robustness, and so on. Give an example of two design goals that
may contradict one another.
11. What is the difference between kernel and user mode? Explain how having two distinct
modes aids in designing an operating system.
12. A 255-GB disk has 65,536 cylinders with 255 sectors per track and 512 bytes per sec-
tor. How many platters and heads does this disk have? Assuming an average cylinder
seek time of 11 msec, average rotational delay of 7 msec. and reading rate of 100
MB/sec, calculate the average time it will take to read 100 KB from one sector.
13. Consider a system that has two CPUs, each CPU having two threads (hyperthreading).
Suppose three programs, P0, P1, and P2, are started with run times of 5, 10 and 20
msec, respectively. How long will it take to complete the execution of these programs?
Assume that all three programs are 100% CPU bound, do not block during execution,
and do not change CPUs once assigned.
14. List some differences between personal computer operating systems and mainframe
operating systems.
15. A computer has a pipeline with four stages. Each stage takes the same time to do its
work, namely, 1 nsec. How many instructions per second can this machine execute?
16. Consider a computer system that has cache memory, main memory (RAM) and disk,
and an operating system that uses virtual memory. It takes 2 nsec to access a word
from the cache, 10 nsec to access a word from the RAM, and 10 msec to access a word
from the disk. If the cache hit rate is 95% and main memory hit rate (after a cache
miss) is 99%, what is the average time to access a word?
17. When a user program makes a system call to read or write a disk file, it provides an
indication of which file it wants, a pointer to the data buffer, and the count. Control is
then transferred to the operating system, which calls the appropriate driver. Suppose
that the driver starts the disk and terminates until an interrupt occurs. In the case of
reading from the disk, obviously the caller will have to be blocked (because there are
no data for it). What about the case of writing to the disk? Need the caller be blocked
awaiting completion of the disk transfer?
18. What is the key difference between a trap and an interrupt?
19. Is there any reason why you might want to mount a file system on a nonempty direc-
tory? If so, what is it?
20. What is the purpose of a system call in an operating system?
21. Give one reason why mounting file systems is a better design option than prefixing
path names with a drive name or number. Explain why file systems are almost always
mounted on empty directories.
22. For each of the following system calls, give a condition that causes it to fail: open,
close, and lseek.
23. What type of multiplexing (time, space, or both) can be used for sharing the following
resources: CPU, memory, SSD/disk, network card, printer, keyboard, and display?
24. Can the
count = write(fd, buffer, nbytes);
call return any value in count other than nbytes? If so, why?
25. A file whose file descriptor is fd contains the following sequence of bytes: 2, 7, 1, 8, 2,
8, 1, 8, 2, 8, 4. The following system calls are made:
lseek(fd, 3, SEEK SET);
read(fd, &buffer, 4);
where the lseek call makes a seek to byte 3 of the file. What does buffer contain after
the read has completed?
26. Suppose that a 10-MB file is stored on a disk on the same track (track 50) in consecu-
tive sectors. The disk arm is currently situated over track number 100. How long will
it take to retrieve this file from the disk? Assume that it takes about 1 msec to move the
arm from one cylinder to the next and about 5 msec for the sector where the beginning
of the file is stored to rotate under the head. Also, assume that reading occurs at a rate
of 100 MB/s.
27. What is the essential difference between a block special file and a character special
file?
28. In the example given in Fig. 1-17, the library procedure is called read and the system
call itself is called read. Is it essential that both of these have the same name? If not,
which one is more important?
29. The client-server model is popular in distributed systems. Can it also be used in a sin-
gle-computer system?
30. To a programmer, a system call looks like any other call to a library procedure. Is it
important that a programmer know which library procedures result in system calls?
Under what circumstances and why?
31. Figure 1-23 shows that a number of UNIX system calls have no Win32 API equiv-
alents. For each of the calls listed as having no Win32 equivalent, what are the conse-
quences for a programmer of converting a UNIX program to run under Windows?
32. A portable operating system is one that can be ported from one system architecture to
another without any modification. Explain why it is infeasible to build an operating
system that is completely portable. Describe two high-level layers that you will have in
designing an operating system that is highly portable.
33. Explain how separation of policy and mechanism aids in building microkernel-based
operating systems.
34. Virtual machines have become very popular for a variety of reasons. Nevertheless,
they have some downsides. Name one.
35. Here are some questions for practicing unit conversions:
(a) How long is a microyear in seconds?
(b) Micrometers are often called microns. How long is a gigamicron?
(c) How many bytes are there in a 1-TB memory?
(d) The mass of the earth is 6000 yottagrams. What is that in grams?
36. Write a shell that is similar to Fig. 1-19 but contains enough code that it actually works
so you can test it. You might also add some features such as redirection of input and
output, pipes, and background jobs.
37. If you have a personal UNIX-like system (Linux, MINIX 3, FreeBSD, etc.) available
that you can safely crash and reboot, write a shell script that attempts to create an
unlimited number of child processes and observe what happens. Before running the
experiment, type sync to the shell to flush the file system buffers to disk to avoid ruin-
ing the file system. You can also do the experiment safely in a virtual machine. Note:
Do not try this on a shared system without first getting permission from the system
administrator. The consequences will be instantly obvious so you are likely to be
caught and sanctions may follow.
38. Examine and try to interpret the contents of a UNIX-like or Windows directory with a
tool like the UNIX od program. (Hint: How you do this will depend upon what the OS
allows. One trick that may work is to create a directory on a USB stick with one oper-
ating system and then read the raw device data using a different operating system that
allows such access.)