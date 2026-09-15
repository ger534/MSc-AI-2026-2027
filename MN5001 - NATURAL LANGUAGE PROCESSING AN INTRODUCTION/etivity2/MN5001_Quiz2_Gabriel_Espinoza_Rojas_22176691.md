<b>1. With the help of an example explain the application of Minimum Edit Distance in one of the following tasks:</b>
<b>a. Spell Correction</b>
<b>b. evaluating Machine Translation</b>
<b>c. evaluating Named Entity Extraction</b>
<b>d. evaluating Speech Recognition</b>

<!-- Pick ONE of the four. Say which one you picked up front.
     Then: what are the two strings being compared? what does the distance
     mean in that context? worked example with actual numbers. -->



<b>2. With the help of an example explain the difference between Hamming distance and Levenshtein Distance</b>

<!-- Key points to cover:
     - Hamming: same-length strings only, counts positions that differ
       (substitutions only, no insertions/deletions)
     - Levenshtein: any lengths, allows insertion + deletion + substitution
     - Give one pair of strings where the two metrics disagree, and show why.
       A single insertion at the front is the clearest case: it shifts every
       later character, so Hamming explodes while Levenshtein stays at 1. -->



<b>3. Explain the advantage of using Dynamic Programming over Recursion for computing the Minimum Edit Distance.</b>

<!-- Key points:
     - naive recursion recomputes the same subproblems many times
       (overlapping subproblems) -> exponential time
     - DP stores each subproblem result once in a table -> O(m*n) time and space
     - You have hard evidence for this from the E-tivity: Task 1 timed the
       recursive version, Task 3 timed the DP version. Quote your own two
       execution times as the example. -->



<b>4. Using the table below, identify the top 3 character pairs which are most likely to be misspelt/typed incorrectly</b>

<!-- The table is Jurafsky's confusion matrix for spelling errors:
     sub[X, Y] = Substitution of X (incorrect) for Y (correct)

     Method: scan the matrix for the three largest counts, and report each as
     an (incorrect, correct) pair with its count. Row = X (what was typed),
     column = Y (what was meant).

     State whether you are treating (a,b) and (b,a) as the same pair or as two
     separate pairs - it changes the answer, and the "explain your counting
     goals" point from Quiz 1 applies here too. -->


| Rank | Typed (X) | Intended (Y) | Count |
|------|-----------|--------------|-------|
| 1    |           |              |       |
| 2    |           |              |       |
| 3    |           |              |       |
