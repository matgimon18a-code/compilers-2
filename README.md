
# Assignment 2 — KPM Algorithm (Token Recognition)
 
**Authors:** Samuel Quintero & Matias Gil
 
**Reference:** Aho, A. V., Lam, M. S., Sethi, R., & Ullman, J. D. *Compilers: Principles, Techniques, and Tools* (2nd ed.). Pearson/Addison Wesley. — Section 3.4.5, Figure 3.20, Exercise 3.4.6 (p. 138)
 
---
 
## How to Run
 
### 1. Clone or download the project
 
Place the file `kmp.py` in your working directory.
 
### 2. Run the script
 
```bash
python kmp.py
```
 
### 3. Expected output
 
The program will automatically:
 
- Display the keyword used: `ababaa`
- Compute and print the **failure function** values for that keyword
- Solve **Exercise 3.4.6 (page 138)** with the two test cases:
  - `a)` text = `abababaab`
  - `b)` text = `abababbaa`
Then it will prompt you to enter a custom text string and keyword to search interactively.
 
### Example session
 
```
Keyword: ababaa
Failure function: [0, 0, 1, 2, 3, 1]
 
Exercise 3.4.6:
 
a) text = abababaab
   Result: yes
 
b) text = abababbaa
   Result: no
 
Enter a text string (or press Enter to exit): hello world
Enter the keyword to search: world
Result: yes
```
 
---
 
## Algorithm Explanation
 
### What is the KMP Algorithm?
 
The **Knuth-Morris-Pratt (KMP)** algorithm is an efficient string-searching algorithm used in the **lexical analysis** phase of a compiler. Its purpose is to determine whether a **keyword (pattern)** appears inside a larger **text string**, which is essential for token recognition.
 
### Failure Function
 
The failure function `f` is a key preprocessing step. Given a pattern `b` of length `n`, it builds an array where `f[s]` stores the length of the longest proper prefix of `b[0..s-1]` that is also a suffix. This allows the algorithm to skip redundant comparisons when a mismatch occurs, instead of restarting from scratch.
 
```
Keyword:          a  b  a  b  a  a
Index (s):        1  2  3  4  5  6
Failure f[s]:     0  0  1  2  3  1
```
 
### KMP Search
 
The main search function scans the text character by character. When a mismatch occurs at position `s` in the pattern, instead of going back in the text, it uses `f[s]` to shift the pattern intelligently, preserving already-matched characters. If `s` reaches `n` (the full length of the pattern), the keyword has been found and the function returns `"yes"`. If the text is exhausted without a full match, it returns `"no"`.
 
This gives the algorithm a time complexity of **O(m + n)**, where `m` is the length of the text and `n` is the length of the pattern, making it significantly more efficient than naïve O(m·n) approaches.
 
---
 
## Exercise 3.4.6 (page 138) — Results
 
Using the keyword `ababaa`:
 
| Case | Text | Found? |
|------|------|--------|
| a) | `abababaab` | **yes** |
| b) | `abababbaa` | **no** |
