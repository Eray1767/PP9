# PP9

## Goal

In this exercise you will:

* Practice using **control structures** (`for`, `if/else`, `switch`) by implementing subprograms.
* Break algorithms into modular C files and design functions with input/output contracts.
* Translate a flowchart (in Mermaid syntax) into working C code.

**Important:** Start a stopwatch when you begin and work uninterruptedly for **90 minutes**. When time is up, stop immediately and record where you paused.

---

## Workflow

1. **Fork** this repository on GitHub.
2. **Clone** your fork locally.
3. Create a `solutions/` directory at the project root:

   ```bash
   mkdir solutions
   ```
4. For each task, add the specified C source files under `solutions/`.
5. **Commit** your changes locally and **push** to GitHub.
6. **Submit** your GitHub repo link for review.

---

## Prerequisites

* GNU C compiler (`gcc`).
* Familiarity with C control structures and function declarations.
* Basic understanding of Mermaid flowchart syntax.

---

## Tasks

### Task 1: Control-Structure Subprograms

**Objective:** Implement three separate C programs, each demonstrating a different control structure.

1. **For Loop**

   * Create `solutions/use_for.c`.
   * Write a function `void count_up(int n)` that uses a `for` loop to print numbers from `1` to `n`, separated by spaces, then a newline.
   * In `main()`, call `count_up(10)`.

2. **If/Else**

   * Create `solutions/use_if.c`.
   * Write a function `const char* sign_of(int x)` that returns:

     * `"positive"` if `x > 0`
     * `"zero"` if `x == 0`
     * `"negative"` otherwise.
   * In `main()`, test `sign_of` on a few values and print the results.

3. **Switch/Case**

   * Create `solutions/use_switch.c`.
   * Write a function `const char* weekday(int d)` mapping `1–7` to day names (`"Monday"`–`"Sunday"`), using a `switch` statement.
   * In `main()`, loop `d` from `1` to `7` and print `weekday(d)`.

**Compile & run each:**

```bash
cc -o solutions/use_for    solutions/use_for.c
cc -o solutions/use_if     solutions/use_if.c
cc -o solutions/use_switch solutions/use_switch.c
./solutions/use_for
./solutions/use_if
./solutions/use_switch
```

---

### Task 2: Flowchart Implementation (Mermaid Diagram)

**Objective:** Translate the following Mermaid flowchart into working C function in its own file.

```mermaid
graph TD
  A[Start: x] --> B[Initialize result = 1]
  B --> C{i = 1 to x?}
  C -- No --> D[Return result]
  C -- Yes --> E{i % 2 == 0?}
  E -- Yes --> F[result += i]
  E -- No --> G[result *= i]
  F --> H[result > 1000?]
  G --> H
  H -- Yes --> I[result -= 100]
  H -- No --> J[Increment i]
  I --> J
  J --> C
```

1. Create `solutions/flowchart_impl.c`.
2. Get an integer `x` passed by value.
3. Implement algorithm as shown:

   * Initialize `result = 1`.
   * Loop `i` from `1` to `x`:

     * If `i` even, add `i`; else multiply.
     * If `result > 1000`, subtract `100`.
   * Print `result`.
4. Compile:

```bash
gcc -c solutions/flowchart_impl solutions/flowchart_impl.c
```
5. Now write a `flowchart_impl.h`, and a `main.c` that calls the function. 

Reflection:

* **Explain how each flowchart node maps to your C code.**
Der Startknoten wird durch das Anlegen der Variablen umgesetzt, der „Initialize result = 1“-Knoten entspricht der Initialisierung von result, die Schleife über i = 1 bis x wird als for‑Schleife implementiert, der Entscheidungs‑Knoten („i even?“) wird durch eine if‑Abfrage (i % 2 == 0) realisiert, die beiden Aktionen („add“ oder „multiply“) sind die jeweiligen Rechenoperationen im Code, die Prüfung „result > 1000“ ist ein weiterer if‑Zweig, und der Endknoten entspricht dem abschließenden printf, der das Ergebnis ausgibt.
---

### Task 3: Code-to-Flowchart

**Objective:** Examine two provided C functions and draw their flowcharts in Mermaid.

1. **Function 1:** `transform_complex(int x)` in `solutions/algorithm_one.c`:

   ```c
   int transform_complex(int x) {
       int result = 1;
       for (int i = 1; i <= x; i++) {
           if (i % 2 == 0) result += i;
           else             result *= i;
           if (result > 1000) result -= 100;
       }
       return result;
   }
   ```
2. **Function 2:** `evaluate_sequence(int *arr, int len)` in `solutions/algorithm_two.c`:

   ```c
   bool evaluate_sequence(int *arr, int len) {
       int state = 0;
       for (int i = 0; i < len; i++) {
           if (arr[i] < 0)       state = -1;
           else if (arr[i] == 0) state = 0;
           else                  state = 1;
           if (state == 1) break;
       }
       switch (state) {
           case 1: return true;
           default: return false;
       }
   }
   ```
3. For each function, draw a **Mermaid** flowchart capturing loops, branches, and switch logic. Include your Mermaid code in a Markdown file under `solutions/`.

**Example Skeleton:**

```mermaid
graph TD
  A[Start] --> B[Initialize]
  B --> C{Condition}
  ...
```
## Flowchart: transform_complex(int x)

```mermaid
flowchart TD

    A([Start]) --> B[Set result = 1]
    B --> C[i = 1]

    C --> D{Is i <= x?}
    D -- No --> Z([Return result])
    D -- Yes --> E{Is i even?}

    E -- Yes --> F[result = result + i]
    E -- No --> G[result = result * i]

    F --> H{result > 1000?}
    G --> H

    H -- Yes --> I[result = result - 100]
    H -- No --> J[No change]

    I --> K[i = i + 1]
    J --> K

    K --> C
````
---

---

## **Flowchart 2 – evaluate_sequence(int *arr, int len)**

```markdown
## Flowchart: evaluate_sequence(int *arr, int len)

```mermaid
flowchart TD

    A([Start]) --> B[Set state = 0]
    B --> C[i = 0]

    C --> D{Is i < len?}
    D -- No --> M[Go to switch(state)]
    D -- Yes --> E{arr[i] < 0?}

    E -- Yes --> F[state = -1]
    E -- No --> G{arr[i] == 0?}

    G -- Yes --> H[state = 0]
    G -- No --> I[state = 1]

    F --> J{state == 1?}
    H --> J
    I --> J

    J -- Yes --> M
    J -- No --> K[i = i + 1]

    K --> C

    M --> N{state == 1?}
    N -- Yes --> O([return true])
    N -- No --> P([return false])
````


**Remember:** Stop after **90 minutes** and record where you stopped.
