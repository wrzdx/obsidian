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

**Biggest Advantage (Плюс):**  
**Скорость переключения.** Переключение потоков делает библиотека (runtime) в пространстве пользователя. Это просто вызов функции. Не нужно делать дорогой System Call, переходить в режим ядра и сбрасывать кэши процессора. Это в 10-100 раз быстрее, чем потоки ядра.

**Biggest Disadvantage (Минус):**  
**Блокирующие системные вызовы.** Если один поток вызовет read() и заблокируется, ядро (не зная о других потоках) остановит **весь процесс**. Все остальные потоки тоже встанут, даже если они готовы работать.

18. In Fig. 2-14 the thread creations and messages printed by the threads are interleaved at
random. Is there a way to force the order to be strictly thread 1 created, thread 1 prints
message, thread 1 exits, thread 2 created, thread 2 prints message, thread 2 exists, and
so on? If so, how? If not, why not?

**Ответ:** **Да, можно.**  
**Как:**  
Родительский процесс должен создавать потоки в цикле и сразу вызывать функцию ожидания завершения (**pthread_join** или аналог).

	1. create(Thread 1)
	2. join(Thread 1) -> Родитель спит, пока Т1 не закончит.
	3. Т1 работает, принтит, делает exit.
	4. Родитель просыпается.
	5. create(Thread 2)...

19. Suppose that a program has two threads, each executing the get account function,
shown below. Identify a race condition in this code.
![600](Pasted%20image%2020251119133323.png)
![600](Pasted%20image%2020251119133344.png)

**Где гонка:**  
В строках обновления массива и инкремента индекса:
    `accounts[account_count] = entered_account; account_count++;`

**Сценарий краша:**
	1. account_count равно 5.
	2. **Поток А** вычисляет адрес accounts\[5\], но еще не записал данные (или записал, но не увеличил счетчик).
	3. **Переключение контекста.**
	4. **Поток Б** читает account_count (оно все еще 5!).
	5. **Поток Б** пишет свои данные в accounts\[5\] (перезаписывая данные Потока А!).
	6. **Поток Б** увеличивает account_count до 6.
	7. **Поток А** просыпается и тоже увеличивает account_count до 7.  
	    **Итог:** Данные А потеряны, в массиве дырка или неверные данные.


20. In the discussion on global variables in threads, we used a procedure create global to
allocate storage for a pointer to the variable, rather than the variable itself. Is this
essential, or could the procedures work with the values themselves just as well?

**Ответ:** Потому что библиотека не знает **размер** данных пользователя.  
Если бы она хранила значения, ей нужно было бы знать: "Вы храните int (4 байта) или огромную структуру (1000 байт)?".  
Храня указатели (void \*), библиотека всегда работает с фиксированным размером (4 или 8 байт), а выделением памяти под саму структуру занимается программист. Это делает библиотеку универсальной.

21. Consider a system in which threads are implemented entirely in user space, with the
run-time system getting a clock interrupt once a second. Suppose that a clock interrupt
occurs exactly while some thread executing in the run-time system is at the point of
blocking or unblocking a thread. What problem might occur? Can you solve it?

**Проблема:**  
Планировщик (Runtime system) — это программа, которая крутит списки очередей (ready list). Если таймер прервет планировщик в момент, когда он переставляет указатели в списке (например, перемещает поток из "Running" в "Ready"), и обработчик сигнала тоже полезет в этот список...  
**Итог:** Список будет разрушен (битые указатели). Программа упадет.  
**Решение:**  
Отключать прерывания (или блокировать сигналы) перед входом в код планировщика и включать обратно при выходе.

22. Suppose that an operating system does not have anything like the select system call to
see in advance if it is safe to read from a file, pipe, or device, but it does allow alarm
clocks (timers) to be set that interrupt blocked system calls. Is it possible to implement
in user space a threads package that will not block all threads when one thread per-
forms a system call that may block? Explain your answer.

**Ответ:** Да.  
**Как:**  
Перед тем как сделать блокирующий вызов (например, read), библиотека потоков ставит таймер (alarm) на короткое время.

1. Если данные есть — read проходит быстро, таймер сбрасывается.
    
2. Если данных нет — read пытается уснуть, но **срабатывает таймер**.
    
3. Сигнал таймера **прерывает** системный вызов read.
    
4. Библиотека ловит прерывание, помечает поток как "ждущий" и переключает управление на другой поток. Позже она попробует снова.

23. Does Peterson’s solution to the mutual-exclusion problem shown in Fig. 2-24 work
when process scheduling is preemptive? How about when it is nonpreemptive?

**Preemptive (Вытесняющая):**  
**Работает.** Процесс А заходит в цикл while, его время истекает, ОС переключает на Процесс Б. Б выходит из критической секции, меняет флаг. А просыпается и заходит. Все ок.

**Nonpreemptive (Невытесняющая):**  
**Не работает (FAIL).**  
Если Процесс А не получил доступ и вошел в цикл активного ожидания (while), он никогда не отдаст процессор. Процесс Б никогда не получит управление, чтобы сбросить флаг.  
**Итог:** Deadlock (или вечный цикл).

24. Can the priority inversion problem discussed in Sec. 2.3.4 happen with user-level
threads? Why or why not?

**Ответ:** Нет (в классическом понимании).  
**Почему:** В User-level threads нет вытеснения по таймеру между потоками внутри процесса.  
Если низкоприоритетный поток (L) захватил мьютекс и работает, высокоприоритетный поток (H) не может "отобрать" у него процессор, пока L сам не отдаст его (thread_yield). Планировщик уровня пользователя знает, что L держит лок, и даст ему доработать.  
Ситуация, когда "Средний (M) вытесняет L, и поэтому H ждет вечно", невозможна, так как M не может вытеснить L без помощи планировщика.

25. In Sec. 2.3.4, a situation with a high-priority process, H, and a low-priority process, L,
was described, which led to H looping forever. Does the same problem occur if round-
robin scheduling is used instead of priority scheduling? Discuss.

**Ответ:** Нет.  
**Почему:**  
В Priority Scheduling процесс M (Medium) работает 100% времени, не давая L (Low) поднять голову. L не может освободить мьютекс. H (High) ждет вечно.  
В **Round Robin** (Карусель) процесс M получит свой квант, но потом **обязательно** уступит место процессу L. L поработает свои 10мс, закончит дело, отпустит мьютекс, и H сможет войти.  
Система будет тормозить, но **не зависнет** намертво.

26. In a system with threads, is there one stack per thread or one stack per process when
user-level threads are used? What about when kernel-level threads are used? Explain.

**User-level threads:**

- 1 стек на каждый поток (в пространстве пользователя). Каждому нужно хранить свои локальные переменные и историю вызовов.
    

**Kernel-level threads:**

- 1 стек на каждый поток в пространстве пользователя.
    
- **ПЛЮС** 1 стек на каждый поток в **ядре** (Kernel stack) — для обработки системных вызовов и прерываний (см. задачу 4).
    

**Итог:** Всегда **один стек на поток** (как минимум). Стек — это суть потока.

27. What is a race condition?

**Гонка данных (Состязание):**  
Ситуация, когда результат работы программы зависит от **случайного порядка выполнения** инструкций в разных процессах/потоках.  
Если процесс А успел раньше — результат правильный. Если Б успел раньше — ошибка. Это баг.

28. When a computer is being developed, it is usually first simulated by a program that
runs one instruction at a time. Even multiprocessors are simulated strictly sequentially
like this. Is it possible for a race condition to occur when there are no simultaneous
events? Explain.

**Вопрос:** Может ли быть гонка, если процессор всего один и выполняет инструкции строго по очереди (даже в симуляторе)?  
**Ответ:** Да.  
**Почему:** Гонка возникает не из-за физической одновременности (параллелизма), а из-за **непредсказуемого чередования (Interleaving)**.  
Симулятор (или одноядерный CPU) выполняет:

1. READ (Поток 1)
    
2. Переключение (симулированное)
    
3. READ (Поток 2)
    
4. WRITE (Поток 2)
    
5. Переключение
    
6. WRITE (Поток 1) — Ошибка! Данные Потока 2 затерты.  
    Для логики программы это ничем не отличается от работы на 100 ядрах.

29. The producer-consumer problem can be extended to a system with multiple producers
and consumers that write (or read) to (from) one shared buffer. Assume that each pro-
ducer and consumer runs in its own thread. Will the solution presented in Fig. 2-28,
using semaphores, work for this system?

**Вопрос:** Будет ли работать схема с рис. 2-28, если производителей и потребителей много?  
**Ответ:** Да, будет работать идеально.  
**Почему:**  
Семафор mutex (бинарный) отвечает за **взаимное исключение**.  
down(&mutex) пускает внутрь критической секции (изменения буфера) **только одного** участника в любой момент времени. Неважно, сколько их толпится снаружи — 2 или 1000. Они встанут в очередь на семафоре, и буфер останется целым.

30. Consider the following solution to the mutual-exclusion problem involving two proc-
esses P0 and P1. Assume that the variable turn is initialized to 0. Process P0’s code is
presented below.
![600](Pasted%20image%2020251119135117.png)
For process P1, replace 0 by 1 in above code. Determine if the solution meets all the
required conditions for a correct mutual-exclusion solution.

**Ответ:** Алгоритм **некорректен**.  
**Почему:** Он нарушает условие **Свобода от блокировки:** Процесс, выполняющийся вне своего критического региона, не должен блокировать любой другой процесс.**

- Алгоритм заставляет процессы строго чередоваться: 0 -> 1 -> 0 -> 1.
    
- Если P0 выйдет из критической секции и пойдет пить кофе (зависнет в Other code надолго), то P1 **никогда** не сможет войти, даже если критическая секция свободна. P1 будет вечно ждать, пока P0 вернется и "передаст эстафету".

31. Show how counting semaphores (i.e., semaphores that can hold an arbitrary value) can
be implemented using only binary semaphores and ordinary machine instructions.

**Задача:** Как сделать считающий семафор, имея только бинарные (мьютексы)?  
**Решение:** Нам нужны:

1. int count (счетчик ресурсов).
2. binary_sem mutex (для защиты переменной count).
3. binary_sem delay (для усыпления потоков, изначально 0 — locked).

**Алгоритм Down:**

1. Захватить mutex.
2. count--.
3. Если count < 0:
    - Отпустить mutex.
    - down(&delay) (Заснуть).
4. Иначе: отпустить mutex.

**Алгоритм Up:**

	1. Захватить mutex.
	2. count++.
	3. Если count <= 0 (значит кто-то спит):
	    - up(&delay) (Разбудить одного).
	4. Отпустить mutex.

32. If a system has only two processes, does it make sense to use a barrier to synchronize
them? Why or why not?

**Ответ:** Да, имеет смысл.  
**Почему:** Если эти два процесса работают в **конвейере** или итеративно (например, симуляция физики: посчитали шаг 1 -> обменялись данными -> посчитали шаг 2).  
Барьер гарантирует, что Процесс А не начнет шаг 2, пока Процесс Б не закончил шаг 1.

33. Can two threads in the same process synchronize using a kernel semaphore if the
threads are implemented by the kernel? What if they are implemented in user space?
Assume that no threads in any other processes have access to the semaphore. Discuss
your answers.

-  **Kernel-level threads:**
    
    - **Да.** Это штатный режим. Один поток уснет, ядро переключит процессор на другой поток того же процесса. Все эффективно.
        
-  **User-level threads:**
    
    - **Да, но это катастрофа.** Если user-thread вызовет системный вызов к семафору ядра и заблокируется, ядро (не зная о других потоках) заблокирует **весь процесс**. Все остальные потоки в этом процессе тоже встанут. Это работает логически, но убивает производительность.

34. Suppose that we have a message-passing system using mailboxes. When sending to a
full mailbox or trying to receive from an empty one, a process does not block. Instead,
it gets an error code back. The process responds to the error code by just trying again,
over and over, until it succeeds. Does this scheme lead to race conditions?

**Ситуация:** Вместо блока (sleep) при ошибке "Full/Empty" процесс пробует снова и снова (retry).  
**Гонка (Race Condition)?** **Нет.**  
**Почему:** Операции send и receive в ядре атомарны. Целостность данных не нарушится.  
**Минус:** Это **Busy Waiting**. Процесс будет жрать 100% CPU впустую, разогревая воздух, пока место не освободится.

35. The CDC 6600 computers could handle up to 10 I/O processes simultaneously using
an interesting form of round-robin scheduling called processor sharing. A process
switch occurred after each instruction, so instruction 1 came from process 1, instruc-
tion 2 came from process 2, etc. The process switching was done by special hardware,
and the overhead was zero. If a process needed T sec to complete in the absence of
competition, how much time would it need if processor sharing was used with n proc-
esses?

**Ситуация:** Переключение процессов после каждой инструкции. Накладных расходов нет (hardware switching).  
**Ответ:**

        `n×Tn×T`
      

.  
**Почему:**  
Если у нас `n` процессов, и процессор выполняет по одной инструкции каждого по кругу, то каждый процесс получает  `1/n` скорости процессора.  
Соответственно, время выполнения увеличивается в `n` раз.

36. Consider the following piece of C code:
```c
void main( ) {
	fork( );
	fork( );
	exit( );
}
```
How many child processes are created upon execution of this program?
**Расчет:**
	
	1. Изначально: 1 процесс (Parent).
	2. Первый fork: Появляется Child1. Всего процессов: 2.    
	3. Второй fork: Выполняется **обоими** (Parent и Child1).
	    - Parent рождает Child2.        
	    - Child1 рождает GrandChild1.  
	        **Итог:** Всего 4 процесса.  
	        **Ответ:** Создано **3 новых** дочерних процесса (всего стало 4).

37. Round-robin schedulers normally maintain a list of all runnable processes, with each
process occurring exactly once in the list. What would happen (scheduling-wise) if a
process occurred twice in the list? Can you think of any reason for allowing this?

**Ситуация:** В списке runnable: A, B, A, C...  
**Что будет:** Процесс А получит **два кванта времени** за один круг.  
**Зачем:** Это примитивный способ реализовать **приоритеты**. Если А важнее Б, добавим его в список дважды — он получит в 2 раза больше CPU.

38. Can a measure of whether a process is likely to be CPU bound or I/O bound be deter-
mined by analyzing source code? How can this be determined at run time?

- Сложно. Можно искать циклы с математикой (CPU) или вызовы read/write/socket (I/O), но компилятор и кэши могут все изменить.  

**В рантайме (Run time):**
- **Легко.** Планировщик смотрит: использовал ли процесс свой квант времени целиком?
    - Использовал весь квант и был вытеснен -> **CPU-bound**.
    - Сам ушел в блок раньше времени -> **I/O-bound**.

39. In the section ‘‘When to Schedule,’’ it was mentioned that sometimes scheduling could
be improved if an important process could play a role in selecting the next process to
run when it blocks. Give a situation where this could be used and explain how.

**Пример:** **Producer-Consumer**.  
Когда Потребитель ждет данных (блокируется), он точно знает, что разблокировать его может только Производитель.  
Имеет смысл сказать планировщику: "Я сплю, передай управление Производителю, чтобы он быстрее дал мне данные". Это называется **Priority Donation** (Передача приоритета) или **Handoff**.

40. Explain how time quantum value and context switching time affect each other, in a
round-robin scheduling algorithm.

**Ответ:** Это баланс между **КПД** и **Отзывчивостью**.  
Пусть `Q` — квант, `C` — время переключения.

- Накладные расходы (потери) = `C/(Q+C)​`.
- Если `Q` большое -> Потери малы (эффективно), но система "лагает" (плохой отклик).
- Если `Q` маленькое -> Отклик мгновенный, но процессор тратит кучу времени на переключения (низкий КПД).
- Правило: `Q` должно быть значительно больше `C`  (обычно `Q≈20..50`мс, `C<1C<1` мс)

41. Measurements of a certain system have shown that the average process runs for a time
T before blocking on I/O. A process switch requires a time S, which is effectively wasted (overhead). For round-robin scheduling with quantum Q, give a formula for the CPU efficiency for each of the following:
(a) Q = $\infty$
(b) Q > T
(c) S < Q < T
(d) Q = S
(e) Q nearly 0

**Answer:** c

41. Five jobs are waiting to be run. Their expected run times are 9, 6, 3, 5, and X. In what
order should they be run to minimize average response time? (Your answer will
depend on X.)
**Answer** – SJF

42. Five batch jobs, A through E, arrive at almost the same time. They have estimated run-
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
Это классическая задача на алгоритмы планирования. На экзамене такие задачи решаются составлением **диаграммы Ганта** (на бумаге рисуешь временную шкалу) или простой математикой.

**Дано:**
5 процессов, пришли одновременно ($t=0$).
Длительность (Burst): A=10, B=6, C=2, D=4, E=8.
Приоритет (5 макс): A=3, B=5, C=2, D=1, E=4.

**Формула:**
Turnaround Time (Оборотное время) = Время завершения - Время прибытия.
Так как все прибыли в $t=0$, то Оборотное время = Времени завершения.

---

(a) Round Robin (Processor Sharing)
*Условие говорит "fair share", что подразумевает модель "Processor Sharing", где все активные процессы делят процессор поровну. Если процессов N, каждый работает со скоростью 1/N.*

1.  **0 мин:** Стартуют все 5 (A, B, C, D, E). Скорость выполнения у каждого = 1/5.
    *   Самый короткий — C (2 мин).
    *   Чтобы выполнить 2 мин работы на скорости 1/5, пройдет $2 \times 5 = 10$ минут реального времени.
    *   **C завершается в 10 мин.**
    *   Остальным тоже зачлось по 2 минуты работы.
    *   Остаток работы: A=8, B=4, D=2, E=6.

2.  **10 мин:** Осталось 4 процесса (A, B, D, E). Скорость = 1/4.
    *   Самый короткий остаток — D (2 мин).
    *   Время: $2 \times 4 = 8$ минут.
    *   **D завершается в $10 + 8 = 18$ мин.**
    *   Остальным зачлось еще по 2 минуты.
    *   Остаток работы: A=6, B=2, E=4.

3.  **18 мин:** Осталось 3 процесса (A, B, E). Скорость = 1/3.
    *   Самый короткий остаток — B (2 мин).
    *   Время: $2 \times 3 = 6$ минут.
    *   **B завершается в $18 + 6 = 24$ мин.**
    *   Остаток работы: A=4, E=2.

4.  **24 мин:** Осталось 2 процесса (A, E). Скорость = 1/2.
    *   Самый короткий остаток — E (2 мин).
    *   Время: $2 \times 2 = 4$ минуты.
    *   **E завершается в $24 + 4 = 28$ мин.**
    *   Остаток работы: A=2.

5.  **28 мин:** Остался 1 процесс (A). Скорость = 1 (полная).
    *   Время: 2 минуты.
    *   **A завершается в $28 + 2 = 30$ мин.**

**Расчет среднего:**
$(10 + 18 + 24 + 28 + 30) / 5 = 110 / 5 = \mathbf{22}$ **минуты**.

---

(b) Priority Scheduling
*Порядок: от высшего приоритета к низшему (5 -> 1). Порядок: B, E, A, C, D.*

1.  **B** (приоритет 5): 0 + 6 = 6. Завершение: **6**.
2.  **E** (приоритет 4): 6 + 8 = 14. Завершение: **14**.
3.  **A** (приоритет 3): 14 + 10 = 24. Завершение: **24**.
4.  **C** (приоритет 2): 24 + 2 = 26. Завершение: **26**.
5.  **D** (приоритет 1): 26 + 4 = 30. Завершение: **30**.

**Расчет среднего:**
$(6 + 14 + 24 + 26 + 30) / 5 = 100 / 5 = \mathbf{20}$ **минут**.

---

(c) First-Come, First-Served (FCFS)
*Порядок как в условии: A, B, C, D, E.*

1.  **A**: 0 + 10 = 10. Завершение: **10**.
2.  **B**: 10 + 6 = 16. Завершение: **16**.
3.  **C**: 16 + 2 = 18. Завершение: **18**.
4.  **D**: 18 + 4 = 22. Завершение: **22**.
5.  **E**: 22 + 8 = 30. Завершение: **30**.

**Расчет среднего:**
$(10 + 16 + 18 + 22 + 30) / 5 = 96 / 5 = \mathbf{19.2}$ **минуты**.

---

(d) Shortest Job First (SJF)
*Порядок: от самого короткого к длинному (C, D, B, E, A).*

1.  **C** (2 мин): 0 + 2 = 2. Завершение: **2**.
2.  **D** (4 мин): 2 + 4 = 6. Завершение: **6**.
3.  **B** (6 мин): 6 + 6 = 12. Завершение: **12**.
4.  **E** (8 мин): 12 + 8 = 20. Завершение: **20**.
5.  **A** (10 мин): 20 + 10 = 30. Завершение: **30**.

**Расчет среднего:**
$(2 + 6 + 12 + 20 + 30) / 5 = 70 / 5 = \mathbf{14}$ **минут**.

*(Как и ожидалось, SJF дает наилучший результат).*


42. A process running on CTSS needs 30 quanta to complete. How many times must it be
swapped in, including the very first time (before it has run at all)?

1 + 2  + 4 + 8 + 16 = 31 – 5 

43. Can you think of a way to save the CTSS priority system from being fooled by random
carriage returns?
**Проблема:** Пользователи обманывают систему: программа делает тяжелые вычисления, а в конце кванта жмет "Enter" (имитация I/O), чтобы система подумала, что это интерактивный процесс, и повысила приоритет.  
**Решение:**  
Планировщик должен смотреть не на факт прерывания ввода-вывода, а на **время использования кванта**.

- Если процесс использовал весь квант (или почти весь, например >90%) и только потом ушел в I/O — считаем его **CPU-bound** и понижаем приоритет (или не повышаем).
    
- Повышать приоритет только тем, кто реально быстро отдает процессор.

44. Consider a real-time system with two voice calls of periodicity 5 msec each with CPU
time per call of 1 msec, and one video stream of periodicity 33 msec with CPU time
per call of 11 msec. Is this system schedulable? Show how you derived your answer.

$\sum \frac{C_{i}}{P_{i}}< 1$ – условие планиеруемости в realtime systems

$\frac{1}{5}  + \frac{1}{5} + \frac{11}{33} = 0.73 < 1$

45. For the above problem, can another video stream be added and have the system still be
schedulable?

$0.73 + \frac{11}{33} = 1.06 > 1$ – unschedulable

46. The aging algorithm with a = 1/2 is being used to predict run times. The previous four
runs, from oldest to most recent, are 40, 20, 40, and 15 msec. What is the prediction of
the next time?

$$Prediction_{new} = a \cdot actual + (1-a)Prediction_{old}$$
Нужно пройтись по цепочке. Предположим, что самое первое предсказание (для первого запуска) было равно первому результату (40), или просто посчитаем рекурсивно.

1. **Run 1:** 40 мс. (Предсказание было, допустим, 40).
2. **Run 2:** 20 мс.  
    Предсказание для него было `40`.  
    Предсказание для следующего:`0.5⋅20+0.5⋅40=10+20=30.
    
3. **Run 3:** 40 мс.  
    Предсказание для него было: `30`
    Предсказание для следующего: `0.5⋅40+0.5⋅30=20+15=350.5⋅40+0.5⋅30=20+15=35`
4. **Run 4:** 15 мс.  
    Предсказание для него было: `35`.  
    Предсказание для следующего: `0.5⋅15+0.5⋅35=7.5+17.5=250.5⋅15+0.5⋅35=7.5+17.5=25`

**Ответ:** Следующее предсказанное время = **25 msec**.


47. A soft real-time system has four periodic events with periods of 50, 100, 200, and 250
msec each. Suppose that the four events require 35, 20, 10, and x msec of CPU time,
respectively. What is the largest value of x for which the system is schedulable?

$\frac{35}{50} + \frac{20}{100} + \frac{10}{200} + \frac{x}{250} = 0.95 + \frac{x}{250} \leq 1 \Rightarrow x= 12.5$
48. Explain why two-level scheduling is commonly used. What advantages does it have
over single-level scheduling?
**В чем суть:**

-  **High-level scheduler (Memory scheduler):** Решает, какие процессы держать в оперативной памяти, а какие выгрузить на диск (Swap). Запускается редко.
    
- . **Low-level scheduler (CPU scheduler):** Решает, какой из процессов в памяти запустить на процессоре. Запускается часто.

**Зачем нужно (Преимущества):**  
Если пустить все процессы в память сразу, начнется **Thrashing** (постоянная подкачка страниц, диск умрет).  
Двухуровневая схема позволяет держать в RAM ровно столько процессов, чтобы CPU был занят, но память не переполнялась. Это эффективнее для управления памятью.

48. A real-time system needs to handle two voice calls that each run every 5 msec and con-
sume 1 msec of CPU time per burst, plus one video at 25 frames/sec, with each frame requiring 20 msec of CPU time. Is this system schedulable? Please explain why or why
not it is schedulable and how you came to that conclusion.


0.2+0.2+0.5=0.9 ≤ 1


49. Consider a system in which it is desired to separate policy and mechanism for the
scheduling of kernel threads. Propose a means of achieving this goal.

**Задача:** Как отделить политику (кто должен работать) от механизма (переключения) для потоков ядра?  
**Проблема:** Ядро управляет потоками, но не знает, какой из них важнее для конкретного приложения (например, поток GUI важнее потока сборщика мусора).

**Предлагаемое решение:**  
Использовать **параметризованный системный вызов** или алгоритм **Scheduler Activations** (Активации планировщика).

1. **Механизм (в ядре):** Планировщик ядра просто выбирает поток с наивысшим "рангом" или приоритетом из списка готовых. У него есть код для переключения контекста.
    
2. **Политика (в пространстве пользователя):** Пользовательский процесс может через системный вызов сообщать ядру параметры для своих потоков.
    
    - Пример: sys_set_thread_priority(thread_id, 10).
        
    - Или более сложный вариант: процесс предоставляет ядру **указатель на переменную** в своей памяти, куда он пишет ID того потока, который он хочет запустить следующим. Ядро перед переключением читает эту переменную и выполняет волю процесса.

50. The readers and writers problem can be formulated in several ways with regard to
which category of processes can be started when. Carefully describe three different
variations of the problem, each one favoring (or not favoring) some category of proc-
esses (e.g., readers or writers). For each variation, specify what happens when a reader
or a writer becomes ready to access the database, and what happens when a process is
finished.

В зависимости от того, кого мы любим больше, алгоритм меняется.

Вариант 1: Readers Preference (Приоритет Читателей)

Классический вариант, описанный в книге.

- **Правило:** Если база занята читателями, и приходит **новый читатель**, он **пускается сразу**.
    
- **Если приходит Писатель:** Он ждет, пока уйдут **все** читатели.
    
- **Итог:** Максимальная параллельность (много читателей одновременно), но **Голодание Писателя** (Writer Starvation). Если поток читателей непрерывен, писатель никогда не зайдет.
    

Вариант 2: Writers Preference (Приоритет Писателей)

- **Правило:** Если пришел (или уже ждет) Писатель, **новые читатели не пускаются**, даже если база сейчас занята другими читателями. Они встают в очередь за писателем.
    
- **Сценарий:** Читает А. Приходит Писатель (ждет А). Приходит Читатель Б (ждет Писателя).
    
- **Итог:** Писатель гарантированно получит доступ быстрее. Устраняется голодание писателя, но снижается производительность чтения.
    

Вариант 3: Fair Access (Справедливая очередь / FIFO)

- **Правило:** Кто первый пришел, тот и обслуживается. Никаких привилегий.
    
- **Реализация:** Все запросы (read и write) встают в одну FIFO очередь.
    
- **Сценарий:**
    
    1. Пришел Читатель А -> Зашел.
        
    2. Пришел Писатель -> Ждет А.
        
    3. Пришел Читатель Б -> Ждет Писателя (хотя мог бы зайти с А, но это нарушило бы порядок).
        
- **Итог:** Никто не голодает, полная справедливость, но **меньшая параллельность** (Читатель Б мог бы читать параллельно с А, но он ждет Писателя).

51. Write a shell script that produces a file of sequential numbers by reading the last num-
ber in the file, adding 1 to it, and then appending it to the file. Run one instance of the
script in the background and one in the foreground, each accessing the same file. How
long does it take before a race condition manifests itself? What is the critical region?
Modify the script to prevent the race. (Hint: use
ln file file.lock
to lock the data file.)
52. Assume that you have an operating system that provides semaphores. Implement a
message system. Write the procedures for sending and receiving messages.
53. Rewrite the program of Fig. 2-23 to handle more than two processes.
54. Write a producer-consumer problem that uses threads and shares a common buffer.
However, do not use semaphores or any other synchronization primitives to guard the
shared data structures. Just let each thread access them when it wants to. Use sleep and
wakeup to handle the full and empty conditions. See how long it takes for a fatal race
condition to occur. For example, you might have the producer print a number once in a
while. Do not print more than one number every minute because the I/O could affect
the race conditions.
55. A process can be put into a round-robin queue more than once to give it a higher prior-
ity. Running multiple instances of a program each working on a different part of a data
pool can have the same effect. First write a program that tests a list of numbers for pri-
mality. Then devise a method to allow multiple instances of the program to run at once
in such a way that no two instances of the program will work on the same number. Can
you in fact get through the list faster by running multiple copies of the program? Note
that your results will depend upon what else your computer is doing; on a personal
computer running only instances of this program you would not expect an
improvement, but on a system with other processes, you should be able to grab a big-
ger share of the CPU this way.
56. Implement a program to count the frequency of words in a text file. The text file is
partitioned into N segments. Each segment is processed by a separate thread that out-
puts the intermediate frequency count for its segment. The main process waits until all
the threads complete; then it computes the consolidated word-frequency data based on
the individual threads’ output.