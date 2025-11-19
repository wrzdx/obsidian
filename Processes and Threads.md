- [Processes](Processes.md)
- [Threads](Threads.md)
- [Event-driven servers](Event-driven%20servers.md)
- [Synchronization and interprocess communication](Synchronization%20and%20interprocess%20communication.md)
- [Scheduling](Scheduling.md)

PROBLEMS
1. In Fig. 2-2, three process states are shown. In theory, with three states, there could be
six transitions, two out of each state. However, only four transitions are shown. Are
there any circumstances in which either or both of the missing transitions might occur?

The transition from blocked to running is conceivable. Suppose that a process is blocked on I/O and the I/O fiinishes. If the CPU is otherwise idle, the process could go directly from blocked to running. The other missing transition, from ready to blocked, is impossible. A ready process cannot do I/O or anything else that might block it. Only a running process can block.

2. Suppose that you were to design an advanced computer architecture that did process
switching in hardware, instead of having interrupts. What information would the CPU
need? Describe how the hardware process switching might work.

- **Инфа:** CPU нужен регистр-указатель на структуру процесса в памяти. Эта структура должна содержать слоты для всех регистров и состояния MMU.
    
- **Механизм:** При срабатывании триггера CPU аппаратно сбрасывает свое состояние в память по указателю "текущего процесса", обновляет указатель на "следующий процесс", загружает состояние оттуда и продолжает работу. Без запуска кода ядра ОС.


3. On all current computers, at least part of the interrupt handlers are written in assembly
language. Why?

Высокоуровневые языки (C/C++) не умеют работать с "сырым" состоянием процессора. Ассемблер необходим для **сохранения всех регистров** прерванного процесса и переключения указателя стека **до того**, как начнет выполняться код на высокоуровневом языке, который может эти регистры испортить

4. When an interrupt or a system call transfers control to the operating system, a kernel
stack area separate from the stack of the interrupted process is generally used. Why?

Безопасность и надежность.

**Пояснение:**  
Когда происходит системный вызов или прерывание, процессор переходит в режим ядра. Если бы он продолжал использовать стек пользователя:

1. **Риск краша:** Указатель стека пользователя (SP) может быть кривым (указывать на несуществующую память). Если ядро попытается туда писать — ОС упадет (Blue Screen).
    
2. **Безопасность:** В стеке могут храниться секретные данные ядра. Если бы они лежали в пользовательском стеке, юзер мог бы их подсмотреть или перезаписать после возврата управления.

5. A computer system has enough room to hold four programs in its main memory. These
programs are idle waiting for I/O half the time. What fraction of the CPU time is
wasted?

**Дано:**

-         `n=4n=4`
    (программы).
-         `p=0.5p=0.5`
    (вероятность, что программа ждет I/O, то есть 50%).
    

**Вопрос:** Какая доля времени CPU тратится впустую (Idle)?

**Решение:**  
CPU простаивает только тогда, когда **ВСЕ** 4 процесса одновременно ждут I/O.  
Формула вероятности одновременного события:  

        `Prob(CPU_Idle)=pnProb(CPU_Idle)=p^n`
        `Prob=0.5^4=0.0625Prob=0.54=0.0625`
      

**Ответ:** **6.25%** (или 1/16) времени процессор простаивает.

6. A computer has 2 GB of RAM of which the operating system occupies 256 MB. The
processes are all 128 MB (for simplicity) and have the same characteristics. If the goal
is 99% CPU utilization, what is the maximum I/O wait that can be tolerated?

Всего процессов $\frac{2 * 10^{3} - 256}{128}= 14$.

CPU_UTILIZATION = $1- p^{n}= 0.99$ 

$p^{n}= 0.01 \rightarrow p \approx 0.72$

**Ответ:** Процессы могут ждать I/O до **~72%** времени, и мы все равно добьемся 99% загрузки.

7. Multiple jobs can run in parallel and finish faster than if they had run sequentially.
Suppose that two jobs, each needing 10 minutes of CPU time, start simultaneously.
How long will the last one take to complete if they run sequentially? How long if they
run in parallel? Assume 50% I/O wait.

**Дано:**

- 2 задачи
- Каждой нужно **10 минут чистого CPU**.
- I/O Wait = 50%.

**Решение:**

**А) Последовательно (Sequentially):**  
Раз I/O занимает 50%, значит процесс работает в два раза дольше, чем требует CPU.  
Время одной задачи =  $10 мин/(1−0.5)=20$минут.  
Две задачи подряд:    $20+20=40$ минут.

**Б) Параллельно (In parallel):**  
Тут вступает формула утилизации CPU.  
При двух процессах (n=2 p=0.5), загрузка процессора будет:  
        $$Util=1−0.5^2=1−0.25=0.75$$

(или 75%).

Это значит, что каждую минуту реального времени процессор выполняет 0.75 минуты полезной работы (для обоих процессов суммарно).  
Общий объем работы CPU для двух задач = 10+10=20 минут.  
Время выполнения =  $\frac{Total CPU Work}{Utilization Rate}=20/0.75=26.67$ минут.

**Ответ:** Последовательно — **40 мин**, Параллельно — **~26.7 мин**.

8. Consider a multiprogrammed system with degree of 5 (i.e., five programs in memory
at the same time). Assume that each process spends 40% of its time waiting for I/O.
What will be the CPU utilization?

$$1 - p^{n}= 1 - 0.4^{5} = 0.98976$$

9. Explain how a Web browser can utilize the concept of threads to improve performance.

**Ответ:** Для **отзывчивости (Responsiveness)** и **параллелизма**.

**Пояснение:**  
Если браузер будет однопоточным:

1. Пока качается HTML, интерфейс "замерзнет" (не нажмешь кнопку "Стоп").
    
2. Картинки будут грузиться по очереди (медленно).
    

С потоками:

- **Thread 1 (UI):** Обрабатывает клики и скроллинг (всегда активен).
    
- **Thread 2 (Network):** Качает данные.
    
- **Thread 3+:** Качают картинки/скрипты параллельно.
    
- **Thread Render:** Рисует страницу.


10. Assume that you are trying to download a large 2-GB file from the Internet. The file is
available from a set of mirror servers, each of which can deliver a subset of the file’s
bytes; assume that a given request specifies the starting and ending bytes of the file.
Explain how you might use threads to improve the download time.

The client process can create separate threads; each thread can fetch a different part of the file from one of the mirror servers. This can help reduce downtime. Of course, there is a single network link being shared by all threads. This link can become a bottleneck as the number of threads becomes very large

11. In the text it was stated that the model of Fig. 2-10(a) was not suited to a file server
using a cache in memory. Why not? Could each process have its own cache?

It would be difϐicult, if not impossible, to keep the ϐile system consistent. Suppose that a client process sends a request to server process 1 to update a ϐile. This process updates the cache entry in its memory. Shortly thereafter, another client process sends a request to server 2 to read that ϐile. Unfortunately, if the ϐile is also cached there, server 2, in its innocence, will return obsolete data. If the ϐirst process writes the ϐile through to the disk after caching it, and server 2 checks the disk on every read to see if its cached copy is up-to-date, the system can be made to work, but it is precisely all these disk accesses that the caching system is trying to avoid.

1. Почему модель "много отдельных процессов" (Fig. 2-10a) плоха для файлового сервера с кэшем?

Суть файлового сервера — быстро отдавать данные. Для этого используется **кэш** в оперативной памяти (буфер недавно считанных файлов).

- **Проблема процессов:** Каждый процесс имеет **свое изолированное адресное пространство**.
    
- **Сценарий:**
    
    1. Процесс А читает файл report.doc с диска и сохраняет его в своей памяти (в своем кэше).
        
    2. Приходит запрос к Процессу Б на тот же файл report.doc.
        
    3. Процесс Б **не видит** память Процесса А.
        
    4. Процесс Б вынужден снова читать файл с медленного диска.
        
- **Итог:** Эффективность кэширования падает до нуля, так как процессы не могут легко делиться загруженными данными. Потоки же (Fig. 2-10b) живут в одном адресном пространстве и видят общий кэш.
    

2. Может ли каждый процесс иметь свой собственный кэш?

	Теоретически — **да**, технически это реализуемо. Но это **ужасное архитектурное решение** по двум причинам:
	
	1. **Трата памяти (Memory Waste):**  
	    Если 100 клиентов запросят один и тот же популярный файл, у вас в памяти будет 100 копий этого файла (по одной в кэше каждого процесса). При общем кэше (в модели с потоками) копия была бы одна. Память сервера закончится моментально.
	    
	2. **Проблема когерентности (Consistency/Coherence):**  
	    Если Процесс А **изменит** файл в своем кэше, Процесс Б об этом не узнает и продолжит отдавать клиентам старую версию из своего кэша. Синхронизировать множество независимых кэшей через IPC (Inter-Process Communication) — это очень сложно и медленно.


12. In Fig. 2-8, a multithreaded Web server is shown. If the only way to read from a file is
the normal blocking read system call, do you think user-level threads or kernel-level
threads are being used for the Web server? Why?

**Ответ:** **Kernel-level (Потоки ядра).**

**Почему:**

- **User-level:** Ядро видит весь процесс как один поток. Если один user-level поток вызовет блокирующий read, ядро заблокирует **весь процесс целиком**. Сервер "зависнет" и не сможет обслуживать других клиентов, пока диск не отдаст данные. Это убивает смысл многопоточности.
    
- **Kernel-level:** Ядро видит каждый поток отдельно. Если один поток заблокируется на read, ядро переключит CPU на другой поток этого же процесса. Сервер продолжит работать.

13. In the text, we described a multithreaded Web server, showing why it is better than a
single-threaded server and a finite-state machine server. Are there any circumstances in
which a single-threaded server might be better? Give an example.

**Ответ:** **Да.**  
**Сценарий:**

1. **Нет блокирующего I/O (или его очень мало):** Все данные уже в кэше (в RAM).
    
2. **Работа ограничена CPU (CPU-bound) и очень короткая.**
    

**Пример:** Простой **Redis** (он однопоточный) или кэширующий DNS-сервер.  
Если сервер просто читает из памяти и отдает в сеть, многопоточность только навредит из-за накладных расходов на переключение контекста и синхронизацию (мьютексы). Один поток, работающий на 100% CPU без переключений, будет быстрее.

14. In Fig. 2-11 the register set is listed as a per-thread rather than a per-process item.
Why? After all, the machine has only one set of registers.

**Ответ:** Потому что каждый поток выполняет **свой код** (или разное место одного кода).
- Когда планировщик останавливает Поток А и запускает Поток Б, он должен **сохранить** состояние Потока А, чтобы потом продолжить с того же места.
    
- Состояние — это и есть значения регистров: **Instruction Pointer (PC)** (где я?), **Stack Pointer** (где мои переменные?) и регистры данных.
    
- Поэтому у каждого потока в таблице потоков есть свое место для хранения "снимка" регистров.

15. Why would a thread ever voluntarily give up the CPU by calling thread yield? After
all, since there is no periodic clock interrupt, it may never get the CPU back.

Это **Cooperative Multitasking (Кооперативная многозадачность)**.  
Поток вызывает yield (сдаюсь), потому что:

1. Он ждет ресурс, который занят другим потоком (например, хочет войти в критическую секцию, но она залочена). Если он не уступит место, тот второй поток никогда не получит CPU, не закончит работу и не освободит ресурс. Будет **Deadlock**.
    
2. Просто из вежливости, если задача очень долгая, чтобы дать поработать другим (в системах без вытеснения).

16. In this problem, you are to compare reading a file using a single-threaded file server
and a multithreaded server. It takes 15 msec to get a request for work, dispatch it, and
do the rest of the necessary processing, assuming that the data needed are in the block
cache. If a disk operation is needed, as is the case one-third of the time, an additional
75 msec is required, during which time the thread sleeps. How many requests/sec can
the server handle if it is single threaded? If it is multithreaded?

**Дано:**

- CPU time (обработка) = 15 мс.
- I/O time (диск) = 75 мс.
- I/O нужен в 1/3 случаев (33%).

**А) Single-threaded (Один поток):**  
Поток делает все последовательно. Среднее время на один запрос:

$$T_{req}​=15+(\frac{1}{3}​×75)=15+25=40\ мс$$
Производительность
$$\frac{1000\ ms }{40\ ms} = 25 \ \frac{req}{sec}$$

**Б) Multithreaded (Много потоков):**  
Пока одни потоки спят на диске (75 мс), другие используют CPU.  
Узкое место — процессор (CPU). Мы можем обрабатывать запросы так быстро, как процессор успевает делать свою часть работы (15 мс). Диск работает "параллельно" (через DMA) и нас не тормозит (предполагаем, что дисков/каналов хватает).  
Производительность ограничена только CPU:  
        $$\frac{1000 мс}{15 мс} ≈ 66.67\frac{ запросов}{сек}$$
17. What is the biggest advantage of implementing threads in user space? What is the big-
gest disadvantage?



18. In Fig. 2-14 the thread creations and messages printed by the threads are interleaved at
random. Is there a way to force the order to be strictly thread 1 created, thread 1 prints
message, thread 1 exits, thread 2 created, thread 2 prints message, thread 2 exists, and
so on? If so, how? If not, why not?
19. Suppose that a program has two threads, each executing the get account function,
shown below. Identify a race condition in this code.
int accounts[LIMIT]; int account count = 0;
void *get account(void *tid) {
char *lineptr = NULL;
size t len = 0;
while (account count < LIMIT)
{
// Read user input from terminal and store it in lineptr
getline(&lineptr, &len, stdin);
// Convert user input to integer
// Assume user entered valid integer value
int entered account = atoi(lineptr);
accounts[account count] = entered account;
account count++;
}CHAP. 2
PROBLEMS
175
// Deallocate memory that was allocated by getline call
free(lineptr);
return NULL; }
20. In the discussion on global variables in threads, we used a procedure create global to
allocate storage for a pointer to the variable, rather than the variable itself. Is this
essential, or could the procedures work with the values themselves just as well?
21. Consider a system in which threads are implemented entirely in user space, with the
run-time system getting a clock interrupt once a second. Suppose that a clock interrupt
occurs exactly while some thread executing in the run-time system is at the point of
blocking or unblocking a thread. What problem might occur? Can you solve it?
22. Suppose that an operating system does not have anything like the select system call to
see in advance if it is safe to read from a file, pipe, or device, but it does allow alarm
clocks (timers) to be set that interrupt blocked system calls. Is it possible to implement
in user space a threads package that will not block all threads when one thread per-
forms a system call that may block? Explain your answer.
23. Does Peterson’s solution to the mutual-exclusion problem shown in Fig. 2-24 work
when process scheduling is preemptive? How about when it is nonpreemptive?
24. Can the priority inversion problem discussed in Sec. 2.3.4 happen with user-level
threads? Why or why not?
25. In Sec. 2.3.4, a situation with a high-priority process, H, and a low-priority process, L,
was described, which led to H looping forever. Does the same problem occur if round-
robin scheduling is used instead of priority scheduling? Discuss.
26. In a system with threads, is there one stack per thread or one stack per process when
user-level threads are used? What about when kernel-level threads are used? Explain.
27. What is a race condition?
28. When a computer is being developed, it is usually first simulated by a program that
runs one instruction at a time. Even multiprocessors are simulated strictly sequentially
like this. Is it possible for a race condition to occur when there are no simultaneous
events? Explain.
29. The producer-consumer problem can be extended to a system with multiple producers
and consumers that write (or read) to (from) one shared buffer. Assume that each pro-
ducer and consumer runs in its own thread. Will the solution presented in Fig. 2-28,
using semaphores, work for this system?
30. Consider the following solution to the mutual-exclusion problem involving two proc-
esses P0 and P1. Assume that the variable turn is initialized to 0. Process P0’s code is
presented below.
/* Other code */
while (turn != 0) { } /* Do nothing and wait. */
Critical Section /* . . . */
turn = 0;
/* Other code */176
PROCESSES AND THREADS
CHAP. 2
For process P1, replace 0 by 1 in above code. Determine if the solution meets all the
required conditions for a correct mutual-exclusion solution.
31. Show how counting semaphores (i.e., semaphores that can hold an arbitrary value) can
be implemented using only binary semaphores and ordinary machine instructions.
32. If a system has only two processes, does it make sense to use a barrier to synchronize
them? Why or why not?
33. Can two threads in the same process synchronize using a kernel semaphore if the
threads are implemented by the kernel? What if they are implemented in user space?
Assume that no threads in any other processes have access to the semaphore. Discuss
your answers.
34. Suppose that we have a message-passing system using mailboxes. When sending to a
full mailbox or trying to receive from an empty one, a process does not block. Instead,
it gets an error code back. The process responds to the error code by just trying again,
over and over, until it succeeds. Does this scheme lead to race conditions?
35. The CDC 6600 computers could handle up to 10 I/O processes simultaneously using
an interesting form of round-robin scheduling called processor sharing. A process
switch occurred after each instruction, so instruction 1 came from process 1, instruc-
tion 2 came from process 2, etc. The process switching was done by special hardware,
and the overhead was zero. If a process needed T sec to complete in the absence of
competition, how much time would it need if processor sharing was used with n proc-
esses?
36. Consider the following piece of C code:
void main( ) {
fork( );
fork( );
exit( );
}
How many child processes are created upon execution of this program?
37. Round-robin schedulers normally maintain a list of all runnable processes, with each
process occurring exactly once in the list. What would happen (scheduling-wise) if a
process occurred twice in the list? Can you think of any reason for allowing this?
38. Can a measure of whether a process is likely to be CPU bound or I/O bound be deter-
mined by analyzing source code? How can this be determined at run time?
39. In the section ‘‘When to Schedule,’’ it was mentioned that sometimes scheduling could
be improved if an important process could play a role in selecting the next process to
run when it blocks. Give a situation where this could be used and explain how.
40. Explain how time quantum value and context switching time affect each other, in a
round-robin scheduling algorithm.
41. Measurements of a certain system have shown that the average process runs for a time
T before blocking on I/O. A process switch requires a time S, which is effectivelyCHAP. 2
PROBLEMS
177
wasted (overhead). For round-robin scheduling with quantum Q, give a formula for
the CPU efficiency for each of the following:
(a) Q = '
(b) Q > T
(c) S < Q < T
(d) Q = S
(e) Q nearly 0
42. Five jobs are waiting to be run. Their expected run times are 9, 6, 3, 5, and X. In what
order should they be run to minimize average response time? (Your answer will
depend on X.)
43. Five batch jobs, A through E, arrive at almost the same time. They have estimated run-
ning times of 10, 6, 2, 4, and 8 minutes. Their (externally determined) priorities are 3,
5, 2, 1, and 4, respectively, with 5 being the highest priority. For each of the following
scheduling algorithms, determine the mean process turnaround time. Ignore process
switching overhead.
(a) Round robin.
(b) Priority scheduling.
(c) First-come, first-served (run in order 10, 6, 2, 4, 8).
(d) Shortest job first.
For (a), assume that the system is multiprogrammed, and that each job gets its fair
share of the CPU. For (b) through (d), assume that only one job at a time runs, until it
finishes. All jobs are completely CPU bound.
44. A process running on CTSS needs 30 quanta to complete. How many times must it be
swapped in, including the very first time (before it has run at all)?
45. Can you think of a way to save the CTSS priority system from being fooled by random
carriage returns?
46. Consider a real-time system with two voice calls of periodicity 5 msec each with CPU
time per call of 1 msec, and one video stream of periodicity 33 msec with CPU time
per call of 11 msec. Is this system schedulable? Show how you derived your answer.
47. For the above problem, can another video stream be added and have the system still be
schedulable?
48. The aging algorithm with a = 1/2 is being used to predict run times. The previous four
runs, from oldest to most recent, are 40, 20, 40, and 15 msec. What is the prediction of
the next time?
49. A soft real-time system has four periodic events with periods of 50, 100, 200, and 250
msec each. Suppose that the four events require 35, 20, 10, and x msec of CPU time,
respectively. What is the largest value of x for which the system is schedulable?
50. Explain why two-level scheduling is commonly used. What advantages does it have
over single-level scheduling?
51. A real-time system needs to handle two voice calls that each run every 5 msec and con-
sume 1 msec of CPU time per burst, plus one video at 25 frames/sec, with each frame178
PROCESSES AND THREADS
CHAP. 2
requiring 20 msec of CPU time. Is this system schedulable? Please explain why or why
not it is schedulable and how you came to that conclusion.
52. Consider a system in which it is desired to separate policy and mechanism for the
scheduling of kernel threads. Propose a means of achieving this goal.
53. The readers and writers problem can be formulated in several ways with regard to
which category of processes can be started when. Carefully describe three different
variations of the problem, each one favoring (or not favoring) some category of proc-
esses (e.g., readers or writers). For each variation, specify what happens when a reader
or a writer becomes ready to access the database, and what happens when a process is
finished.
54. Write a shell script that produces a file of sequential numbers by reading the last num-
ber in the file, adding 1 to it, and then appending it to the file. Run one instance of the
script in the background and one in the foreground, each accessing the same file. How
long does it take before a race condition manifests itself? What is the critical region?
Modify the script to prevent the race. (Hint: use
ln file file.lock
to lock the data file.)
55. Assume that you have an operating system that provides semaphores. Implement a
message system. Write the procedures for sending and receiving messages.
56. Rewrite the program of Fig. 2-23 to handle more than two processes.
57. Write a producer-consumer problem that uses threads and shares a common buffer.
However, do not use semaphores or any other synchronization primitives to guard the
shared data structures. Just let each thread access them when it wants to. Use sleep and
wakeup to handle the full and empty conditions. See how long it takes for a fatal race
condition to occur. For example, you might have the producer print a number once in a
while. Do not print more than one number every minute because the I/O could affect
the race conditions.
58. A process can be put into a round-robin queue more than once to give it a higher prior-
ity. Running multiple instances of a program each working on a different part of a data
pool can have the same effect. First write a program that tests a list of numbers for pri-
mality. Then devise a method to allow multiple instances of the program to run at once
in such a way that no two instances of the program will work on the same number. Can
you in fact get through the list faster by running multiple copies of the program? Note
that your results will depend upon what else your computer is doing; on a personal
computer running only instances of this program you would not expect an
improvement, but on a system with other processes, you should be able to grab a big-
ger share of the CPU this way.
59. Implement a program to count the frequency of words in a text file. The text file is
partitioned into N segments. Each segment is processed by a separate thread that out-
puts the intermediate frequency count for its segment. The main process waits until all
the threads complete; then it computes the consolidated word-frequency data based on
the individual threads’ output.