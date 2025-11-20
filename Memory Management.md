- [No Memory Abstraction (Без абстракции памяти)](No%20Memory%20Abstraction%20(Без%20абстракции%20памяти).md)
- [A Memory Abstraction Address Spaces (Адресные пространства)](A%20Memory%20Abstraction%20Address%20Spaces%20(Адресные%20пространства).md)
- [Virtual Memory](Virtual%20Memory.md)
- [Page Replacement Algorithms](Page%20Replacement%20Algorithms.md)
- [Design Issues for Paging Systems (Проблемы проектирования)](Design%20Issues%20for%20Paging%20Systems%20(Проблемы%20проектирования).md)
- [Implementation Issues (Проблемы реализации)](Implementation%20Issues%20(Проблемы%20реализации).md)
- [Segmentation](Segmentation.md)
- [Researches and summary](Researches%20and%20summary.md) 

---

### 1. Base and Limit Registers
**Question:** In Fig. 3-3 the base and limit registers contain the same value, 16,384. Is this just an accident, or are they always the same? If it is not an accident, why are they the same in this example?

**Пояснение:** На рисунке показана ситуация, когда в памяти лежат две программы подряд. Первая занимает 16 КБ (от 0 до 16384), вторая — тоже 16 КБ (от 16384 до 32768).
*   **Base register** хранит адрес начала программы. Для второй программы это 16384.
*   **Limit register** хранит *размер* программы. Для второй программы это тоже 16384.

**Ответ:**
Это случайность (Coincidence).
В этом примере вторая программа просто начинается ровно там, где заканчивается первая (на адресе 16384), и имеет длину ровно 16384 байта.
Если бы вторая программа была короче (например, 10 КБ) или длиннее, значения регистров были бы разными. Base указывает на физическое начало, Limit — на длину.

---

### 2. Bitmap vs Linked List
**Question:** In this problem, you are to compare the storage needed to keep track of free memory using a bitmap versus using a linked list. The 8-GB memory is allocated in units of $n$ bytes. For the linked list, assume that memory consists of an alternating sequence of segments and holes, each 1 MB. Also assume that each node in the linked list needs a 32-bit memory address, a 16-bit length, and a 16-bit next-node field. How many bytes of storage is required for each method? Which one is better?

**Решение:**

**А) Linked List (Связный список):**
1.  Размер одного узла: $32 + 16 + 16 = 64$ бита = **8 байт**.
2.  Структура памяти: 8 ГБ RAM, чередуются 1 МБ процесс и 1 МБ дырка.
    $$Total\_Chunks = \frac{8 \text{ GB}}{1 \text{ MB}} = \frac{8192 \text{ MB}}{1 \text{ MB}} = 8192$$
    Это значит, у нас 8192 записи в списке (половина P, половина H).
3.  Общий размер списка:
    $$Size_{list} = 8192 \times 8 \text{ bytes} = 64 \text{ KB}$$

**Б) Bitmap (Битовая карта):**
1.  Память 8 ГБ. Размер блока $n$ байт.
2.  Количество блоков: $\frac{8 \text{ GB}}{n}$.
3.  На каждый блок нужен 1 бит.
4.  Размер битмапа в **байтах**:
    $$Size_{bitmap} = \frac{8 \times 2^{30} \text{ bytes}}{n \times 8 \text{ bits per byte}} = \frac{2^{30}}{n} \text{ bytes}$$

**В) Что лучше?**
Список всегда занимает **64 КБ**.
Битмап зависит от $n$.
Если $n$ маленькое (например, 4 КБ или меньше), битмап будет огромным.
Если $n$ большое, битмап станет меньше.
Битмап станет лучше списка, только если:
$$\frac{2^{30}}{n} < 65536 \Rightarrow n > \frac{2^{30}}{2^{16}} \Rightarrow n > 16 \text{ KB}$$
**Вывод:** Для мелких блоков ($n < 16$ КБ) список экономичнее. Для крупных ($n > 16$ КБ) — битмап.

---

### 3. Allocation Algorithms
**Question:** Consider a swapping system in which memory consists of the following hole sizes in memory order: 10 MB, 4 MB, 20 MB, 18 MB, 7 MB, 9 MB, 12 MB, and 15 MB. Which hole is taken for successive segment requests of (a) 12 MB, (b) 10 MB, (c) 9 MB for first fit? Now repeat the question for best fit, worst fit, and next fit.

**Пояснение:** Слово "successive" (последовательные) означает, что мы изменяем список после каждого шага.
Изначальный список: `[10, 4, 20, 18, 7, 9, 12, 15]`

**1. First Fit (Первый подходящий):**
*   (a) **12 MB:** Ищем первую дырку $\ge$ 12. Это **20 MB**. (Остаток 8).
    *   *Список:* `[10, 4, 8, 18, 7, 9, 12, 15]`
*   (b) **10 MB:** Ищем первую $\ge$ 10. Это **10 MB**. (Остаток 0).
    *   *Список:* `[4, 8, 18, 7, 9, 12, 15]`
*   (c) **9 MB:** Ищем первую $\ge$ 9. Это **18 MB**. (Остаток 9).

**2. Best Fit (Лучший подходящий — самый маленький, но достаточный):**
*Сбрасываем список:* `[10, 4, 20, 18, 7, 9, 12, 15]`
*   (a) **12 MB:** Идеально подходит **12 MB**.
    *   *Список:* `[10, 4, 20, 18, 7, 9, 15]`
*   (b) **10 MB:** Идеально подходит **10 MB**.
    *   *Список:* `[4, 20, 18, 7, 9, 15]`
*   (c) **9 MB:** Идеально подходит **9 MB**.

**3. Worst Fit (Худший подходящий — самый большой):**
*Сбрасываем список:* `[10, 4, 20, 18, 7, 9, 12, 15]`
*   (a) **12 MB:** Самая большая **20 MB**. (Остаток 8).
    *   *Список:* `[10, 4, 8, 18, 7, 9, 12, 15]`
*   (b) **10 MB:** Самая большая **18 MB**. (Остаток 8).
    *   *Список:* `[10, 4, 8, 8, 7, 9, 12, 15]`
*   (c) **9 MB:** Самая большая **15 MB**. (Остаток 6).

**4. Next Fit (Следующий подходящий):**
*Как First Fit, но запоминаем позицию.*
*Сбрасываем список:* `[10, 4, 20, 18, 7, 9, 12, 15]`
*   (a) **12 MB:** Берем **20 MB**. (Индекс 2). Стрелка остается на остатке (8 MB).
    *   *Список:* `[10, 4, 8, 18, 7, 9, 12, 15]`
*   (b) **10 MB:** Начинаем поиск с индекса 2 (там 8 MB - мало). Следующая **18 MB**. Берем её. (Индекс 3).
    *   *Список:* `[10, 4, 8, 8, 7, 9, 12, 15]`
*   (c) **9 MB:** Начинаем с индекса 3 (там 8 MB - мало). Идем дальше: 7, 9, 12... Берем **9 MB**.

---

### 4. Automatic Overlays
**Question:** The first overlay managers and overlay sections were written by hand by programmers. In principle, could this be done automatically by the compiler for a system with limited memory? If so, how, and what difficulties would arise?

**Ответ:**
Да, в принципе это возможно.
**Как:** Компилятор строит граф вызовов (Call Graph). Если Функция А вызывает Б, они должны быть в памяти одновременно. Если Функция А вызывает Б или В (ветвление `if`), но Б и В никогда не вызываются одновременно, они могут перекрывать друг друга (быть в одном оверлее).
**Трудности:**
1.  **Рекурсия:** Сложно предсказать глубину стека.
2.  **Указатели на функции:** Компилятор не всегда знает, какая именно функция будет вызвана по указателю в runtime.

---

### 5. Overlays today
**Question:** In what situations in modern computing might an overlay-style memory system be effective, and why?

**Ответ:**
В **Embedded Systems (Встраиваемые системы)** и IoT.
Там часто используются дешевые микроконтроллеры, где мало памяти (SRAM) и нет MMU (нет поддержки виртуальной памяти). Там программисты до сих пор вручную управляют загрузкой модулей, чтобы сэкономить байты.

---

### 6. Physical vs Virtual Address
**Question:** What is the difference between a physical address and a virtual address?

**Ответ:**
*   **Виртуальный адрес:** Генерируется процессором (программой). Программа "думает", что у неё есть непрерывная память от 0 до N.
*   **Физический адрес:** Реальный адрес на шине памяти, указывающий на конкретную ячейку в микросхеме RAM.
Преобразованием занимается MMU.

---

### 7. Page Number & Offset
**Question:** For each of the following decimal virtual addresses, compute the virtual page number and offset for a 4-KB page and for an 8-KB page: 20000, 32768, 60000.

**Решение:**
Формулы:
$VPN = Address / PageSize$ (целая часть)
$Offset = Address \% PageSize$ (остаток)

**Для 4 KB (4096 байт):**
1.  **20000:** $20000 / 4096 = \mathbf{4}$ (VPN), остаток $\mathbf{3616}$ (Offset).
2.  **32768:** $32768 / 4096 = \mathbf{8}$ (VPN), остаток $\mathbf{0}$ (Offset).
3.  **60000:** $60000 / 4096 = \mathbf{14}$ (VPN), остаток $\mathbf{2656}$ (Offset).

**Для 8 KB (8192 байт):**
1.  **20000:** $20000 / 8192 = \mathbf{2}$ (VPN), остаток $\mathbf{3616}$ (Offset).
2.  **32768:** $32768 / 8192 = \mathbf{4}$ (VPN), остаток $\mathbf{0}$ (Offset).
3.  **60000:** $60000 / 8192 = \mathbf{7}$ (VPN), остаток $\mathbf{2656}$ (Offset).

---

### 8. Address Translation (Fig. 3-9)
**Question:** Using the page table of Fig. 3-9, give the physical address corresponding to each of the following virtual addresses: (a) 2000, (b) 8200, (c) 16536.

*Примечание: Используем данные из рис. 3-9. Там:*
*   Virtual Page 0 -> Physical Frame 2 (Start: 8192)
*   Virtual Page 1 -> Physical Frame 1 (Start: 4096)
*   Virtual Page 2 -> Physical Frame 6 (Start: 24576)
*   Virtual Page 3 -> Physical Frame 0 (Start: 0)
*   Virtual Page 4 -> Physical Frame 4 (Start: 16384)

**Решение:**
(a) **2000**:
*   Это Page 0. Offset 2000.
*   Physical = Frame 2 start + 2000 = $8192 + 2000 = \mathbf{10192}$.

(b) **8200**:
*   Это Page 2 (т.к. $8200 / 4096 = 2$). Offset = $8200 - 8192 = 8$.
*   Physical = Frame 6 start + 8 = $24576 + 8 = \mathbf{24584}$.

(c) **16536**:
*   Это Page 4 (т.к. $16536 / 4096 = 4$, остаток 152).
*   Physical = Frame 4 start + 152 = $16384 + 152 = \mathbf{16536}$. *(Да, совпало с виртуальным, так бывает, если VP 4 мапится на Frame 4).*

---

### 9. Hardware Support
**Question:** What kind of hardware support is needed for a paged virtual memory to work?

**Ответ:**
1.  **MMU (Memory Management Unit):** Для трансляции адресов на лету.
2.  **TLB (Translation Lookaside Buffer):** Кэш для ускорения трансляции.
3.  **Page Table Base Register:** Регистр, указывающий, где в памяти лежит таблица страниц текущего процесса.
4.  **Trap / Fault mechanism:** Возможность прерывать процессор при обращении к отсутствующей странице (Page Fault).

---

### 10. TLB Misses
**Question:** Consider the following C program:
`{c}int X[N]; int step = M; for (int i = 0; i < N; i += step) X[i] = X[i] + 1;`
(a) If this program is run on a machine with a 4-KB page size and 64-entry TLB, what values of M and N will cause a TLB miss for every execution of the inner loop?
(b) Would your answer in part (a) be different if the loop were repeated many times?

**Решение (a):**
Условие "TLB miss for every execution" означает, что каждое обращение `X[i]` должно попадать в **новую** страницу, которой еще нет в TLB.
*   Страница = 4 КБ = 4096 байт.
*   `int` = 4 байта.
*   На одной странице помещается $4096 / 4 = 1024$ целых числа.
*   Чтобы каждый следующий доступ `i += step` попадал на *следующую* страницу, шаг $M$ должен быть не меньше размера страницы в элементах.
    $$M \ge 1024$$
*   $N$ (размер массива) просто должен быть достаточно большим, чтобы цикл запустился.

**Решение (b):**
Да, ответ изменится.
Если мы повторяем цикл много раз:
*   TLB имеет 64 записи. Он может запомнить адреса для 64 страниц.
*   $64 \text{ pages} \times 4 \text{ KB} = 256 \text{ KB}$.
*   Если весь массив $X$ влезает в 256 КБ (то есть $N \times 4 < 256000$, или $N < 65536$), то при втором проходе цикла все страницы уже будут в TLB -> будут сплошные **TLB Hits**.
*   Чтобы промахи были **всегда** (даже при повторах), массив должен быть больше размера TLB ($N > 65536$), чтобы новые страницы вытесняли старые.

