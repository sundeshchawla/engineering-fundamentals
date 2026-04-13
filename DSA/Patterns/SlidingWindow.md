## Variable Size Sliding Window

Core idea: right pointer always moves forward.
Left pointer moves forward ONLY to fix a constraint violation.
The window shrinks until valid, then right pointer
can safely advance again.

When to use: longest/shortest subarray/substring
satisfying some condition.

Template:
int j = 0;
for (int i = 0; i < n; i++) {
    // add s[i] to window
    while (window violates constraint) {
        // remove s[j] from window
        j++;
    }
    // window is valid here — update answer
    ans = max(ans, i - j + 1);
}

Key distinction from Fixed Size window:
Fixed: window size is given (k). Slide rigidly.
Variable: window size is the answer itself. Expand greedily,
          shrink only when forced.

## Problems using this pattern
- Longest Substring No Repeating → shrink when duplicate found
- Minimum Size Subarray Sum → shrink when sum >= target
- Longest Repeating Character Replacement → shrink when
  (window size - max frequency) > k


## The shrink trigger rule — most important thing to memorise

while (window is INVALID) → shrink to RESTORE validity
  → you are maximising the window (finding longest)
  → update answer AFTER the while loop

while (window is VALID) → shrink to SQUEEZE further
  → you are minimising the window (finding shortest)
  → update answer INSIDE the while loop

Getting these two backwards is the most common
sliding window bug in interviews.