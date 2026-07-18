# Time Complexity in Algorithms — Complete Notes

## 1. Introduction

When we write an algorithm, we usually care about two things:
- **Correctness** – does it produce the right output?
- **Efficiency** – how fast does it run, and how much memory does it use?

**Time Complexity** is a way of describing how the **running time of an algorithm grows** as the size of the input (usually denoted `n`) grows. It does **not** measure actual time in seconds (since that depends on hardware, compiler, language, etc.), but instead measures the **number of basic operations** performed as a function of input size.

---

## 2. Why Time Complexity Matters

- Helps compare algorithms **independent of hardware/language**.
- Helps predict how an algorithm behaves for **large inputs**.
- Helps choose the **best algorithm** for a problem before implementing it.
- Essential for technical interviews and competitive programming.

---

## 3. Types of Time Complexity Analysis

| Type | Meaning |
|---|---|
| **Best Case** | Minimum time taken (most favorable input) |
| **Average Case** | Expected time over all possible inputs |
| **Worst Case** | Maximum time taken (least favorable input) |

> In practice, we mostly analyze the **worst case**, because it gives a guarantee — the algorithm will never perform worse than this.

---

## 4. Asymptotic Notations

These notations describe the **growth rate** of an algorithm's running time as `n → ∞`.

### 4.1 Big O Notation — O( )
Represents the **upper bound** (worst case). It tells us the algorithm will not take more time than this.

> f(n) = O(g(n)) if there exist constants `c > 0` and `n₀` such that
> `f(n) ≤ c·g(n)` for all `n ≥ n₀`

**Example:** If an algorithm takes `3n² + 5n + 2` operations, we say it is `O(n²)`.

### 4.2 Omega Notation — Ω( )
Represents the **lower bound** (best case). The algorithm will take **at least** this much time.

> f(n) = Ω(g(n)) if there exist constants `c > 0` and `n₀` such that
> `f(n) ≥ c·g(n)` for all `n ≥ n₀`

### 4.3 Theta Notation — Θ( )
Represents the **tight bound** — both upper and lower bound are the same order.

> f(n) = Θ(g(n)) if f(n) = O(g(n)) **and** f(n) = Ω(g(n))

### Quick Analogy
| Notation | Meaning | Everyday analogy |
|---|---|---|
| O(g(n)) | Worst case (≤) | "At most this much time" |
| Ω(g(n)) | Best case (≥) | "At least this much time" |
| Θ(g(n)) | Average/tight (=) | "Exactly around this much time" |

---

## 5. Common Time Complexities (Fastest → Slowest)

| Complexity | Name | Example Algorithm |
|---|---|---|
| O(1) | Constant | Accessing an array element |
| O(log n) | Logarithmic | Binary Search |
| O(n) | Linear | Linear Search, Traversing an array |
| O(n log n) | Linearithmic | Merge Sort, Quick Sort (avg), Heap Sort |
| O(n²) | Quadratic | Bubble Sort, Selection Sort, Insertion Sort |
| O(n³) | Cubic | Matrix Multiplication (naive) |
| O(2ⁿ) | Exponential | Recursive Fibonacci, Subset generation |
| O(n!) | Factorial | Traveling Salesman (brute force), Permutations |

### Growth Rate Order (increasing):
```
O(1) < O(log n) < O(n) < O(n log n) < O(n²) < O(n³) < O(2ⁿ) < O(n!)
```

---

## 6. Calculating Time Complexity — Rules of Thumb

1. **Loops:** A single loop running `n` times → O(n).
2. **Nested Loops:** Two nested loops each running `n` times → O(n²).
3. **Sequential Statements:** Add the complexities.
   ```
   O(n) + O(n²) = O(n²)   (keep the dominant term)
   ```
4. **Conditional (if-else):** Take the **larger** complexity of the branches.
5. **Drop Constants:** O(2n) → O(n); O(500) → O(1).
6. **Drop Lower Order Terms:** O(n² + n) → O(n²).
7. **Logarithmic behavior:** Appears when the problem size is **divided** (e.g., halved) each step — as in Binary Search, Divide & Conquer.

---

## 7. Examples

### Example 1: Constant Time — O(1)
```python
def get_first(arr):
    return arr[0]
```
Only one operation, regardless of array size.

### Example 2: Linear Time — O(n)
```python
def print_all(arr):
    for x in arr:
        print(x)
```
Loop runs `n` times → O(n).

### Example 3: Quadratic Time — O(n²)
```python
def print_pairs(arr):
    for i in arr:
        for j in arr:
            print(i, j)
```
Nested loop → n × n = O(n²).

### Example 4: Logarithmic Time — O(log n)
```python
def binary_search(arr, target):
    low, high = 0, len(arr) - 1
    while low <= high:
        mid = (low + high) // 2
        if arr[mid] == target:
            return mid
        elif arr[mid] < target:
            low = mid + 1
        else:
            high = mid - 1
    return -1
```
Each step halves the search space → O(log n).

### Example 5: Linearithmic Time — O(n log n)
Merge Sort divides the array (log n levels) and merges at each level in O(n) → total O(n log n).

---

## 8. Time Complexity of Common Algorithms

| Algorithm | Best Case | Average Case | Worst Case |
|---|---|---|---|
| Linear Search | O(1) | O(n) | O(n) |
| Binary Search | O(1) | O(log n) | O(log n) |
| Bubble Sort | O(n) | O(n²) | O(n²) |
| Insertion Sort | O(n) | O(n²) | O(n²) |
| Selection Sort | O(n²) | O(n²) | O(n²) |
| Merge Sort | O(n log n) | O(n log n) | O(n log n) |
| Quick Sort | O(n log n) | O(n log n) | O(n²) |
| Heap Sort | O(n log n) | O(n log n) | O(n log n) |
| Binary Search Tree (avg) | O(log n) | O(log n) | O(n) |
| Hash Table (avg) | O(1) | O(1) | O(n) |

---

## 9. Space Complexity (Related Concept)

Space Complexity measures the **amount of memory** an algorithm uses relative to input size, including:
- Input storage
- Auxiliary/temporary variables
- Recursion call stack

Example: Recursive Fibonacci uses O(n) space due to the call stack, whereas an iterative version uses O(1) space.

---

## 10. Recurrence Relations (for Recursive Algorithms)

Recursive algorithms are analyzed using **recurrence relations**, often solved using the **Master Theorem**.

**Master Theorem** for recurrences of the form:
```
T(n) = a·T(n/b) + f(n)
```
where `a ≥ 1`, `b > 1`:

| Condition | Result |
|---|---|
| f(n) = O(n^(log_b a - ε)) | T(n) = Θ(n^(log_b a)) |
| f(n) = Θ(n^(log_b a)) | T(n) = Θ(n^(log_b a) · log n) |
| f(n) = Ω(n^(log_b a + ε)) | T(n) = Θ(f(n)) |

**Example:** Merge Sort → T(n) = 2T(n/2) + O(n) → falls in case 2 → **T(n) = O(n log n)**

---

## 11. Summary Cheat Sheet

- **Big O** → worst case (most commonly used)
- **Omega** → best case
- **Theta** → average/tight bound
- Always **drop constants** and **lower-order terms**
- Nested loops multiply; sequential code adds (keep the max)
- Divide-and-conquer often gives **O(n log n)**
- Brute-force/recursive-without-memoization often gives **exponential** complexity

---

## 12. Quick Revision Table

| n | O(1) | O(log n) | O(n) | O(n log n) | O(n²) | O(2ⁿ) |
|---|---|---|---|---|---|---|
| 10 | 1 | ~3 | 10 | ~33 | 100 | 1024 |
| 100 | 1 | ~7 | 100 | ~664 | 10,000 | huge |
| 1000 | 1 | ~10 | 1000 | ~9966 | 1,000,000 | astronomically huge |

This table shows why choosing the right algorithm matters enormously as `n` grows.
