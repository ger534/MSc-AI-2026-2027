<b>1. With the help of an example explain the application of Minimum Edit Distance in one of the following tasks:</b>
<b>a. Spell Correction</b>
<b>b. evaluating Machine Translation</b>
<b>c. evaluating Named Entity Extraction</b>
<b>d. evaluating Speech Recognition</b>

<!-- Then: what are the two strings being compared? what does the distance
     mean in that context? worked example with actual numbers. -->

In spell correction, when an user makes a typo, the Minimum Edit Distance allows to find the closest word (minimal number of edits) that should substitute it. Professor Jurasky used the example calculating the similarity to the input 'graffe', with possible words being 'graph' or 'giraffe'. (video 2 1 Defining Minimum Edit Distance 7 04)

<b>2. With the help of an example explain the difference between Hamming distance and Levenshtein Distance</b>

<!-- Key points to cover:
     - Hamming: same-length strings only, counts positions that differ
       (substitutions only, no insertions/deletions)
     - Levenshtein: any lengths, allows insertion + deletion + substitution
     - Give one pair of strings where the two metrics disagree, and show why.
       A single insertion at the front is the clearest case: it shifts every
       later character, so Hamming explodes while Levenshtein stays at 1. -->

The hamming distance only allows substitutions. The Levenshtein distance allows for also insertions and deletions. 

Ben Langmead, in his video (ADS1: Solving the edit distance problem https://youtu.be/8Q2IEIY2pDU?t=205), uses the example

X: GCGTATGCGGCTAACGC
Y: GCTATGCGGCTATACGC

Where he explains that the hamming requires 10 editions, but the Levenshtein distance requires only 2 editions. 

Hamming:
substitution 1:  GCTTATGCGGCTAACGC (index 2)
substitution 2:  GCTAATGCGGCTAACGC (index 3)
substitution 3:  GCTATTGCGGCTAACGC (index 4)
substitution 4:  GCTATGGCGGCTAACGC (index 5)
substitution 5:  GCTATGCCGGCTAACGC (index 6)
substitution 6:  GCTATGCGGGCTAACGC (index 7)
substitution 7:  GCTATGCGGCCTAACGC (index 9)
substitution 8:  GCTATGCGGCTTAACGC (index 10)
substitution 9:  GCTATGCGGCTAAACGC (index 11)
substitution 10: GCTATGCGGCTATACGC (index 12)


Levenshtein:
edit 1, delete G: GC[G]TATGCGGCTAACGC -> GC[ ]TATGCGGCTAACGC
edit 2, add T: GCTATGCGGCTA[T]ACGC -> GCTATGCGGCTATACGC

<b>3. Explain the advantage of using Dynamic Programming over Recursion for computing the Minimum Edit Distance.</b>

<!-- Key points:
     - naive recursion recomputes the same subproblems many times
       (overlapping subproblems) -> exponential time
     - DP stores each subproblem result once in a table -> O(m*n) time and space
     - You have hard evidence for this from the E-tivity: Task 1 timed the
       recursive version, Task 3 timed the DP version. -->

Dynamic programming (which is arguably the first algorithm named with marketing intentions, Professor Jurasky explains), is way faster than recursion. 

In Ben Langmead video (ADS1: Practical: Implementing dynamic programming for edit distance), he and his friends show the difference in performance over the example <code>x = 'shake spea'</code> and <code>y = 'Shakespear'</code>. With <code>editDistRecursive(x,y) Wall time: 5.76 seconds</code> and <code>editDistanceDynamicProgramming(x,y) Wall time: 200 microseconds</code>. Recursion calls itself even when the are no new operations to perform (redundant work), dynamic programming instead uses a matrix that will remember the distances between prefixes to avoid redundant work. 

<b>4. Using the table below, identify the top 3 character pairs which are most likely to be misspelt/typed incorrectly</b>

<!-- The table is Jurafsky's confusion matrix for spelling errors:
     sub[X, Y] = Substitution of X (incorrect) for Y (correct)

     Method: scan the matrix for the three largest counts, and report each as
     an (incorrect, correct) pair with its count. Row = X (what was typed),
     column = Y (what was meant).

     State whether you are treating (a,b) and (b,a) as the same pair or as two
     separate pairs - it changes the answer, and the "explain your counting
     goals" point from Quiz 1 applies here too. -->

The best example for this I found in 2 4 Weighted Minimum Edit Distance 2 47 (https://youtu.be/gx7Fkf1n_5w?t=23)

| Rank | Typed (X) | Intended (Y) | Count |
|------|-----------|--------------|-------|
| 1    |   e   |  a  |   388  |
| 2    |   a   |  e  |   342  |
| 3    |   m   |  n  |   180  |

The top 3 characters most typed incorrectly are:
- a are confused with e (388), i (103) and o (91)
- e are confused with a (342), i (146) and o (116)
- n are confused with m (180)

