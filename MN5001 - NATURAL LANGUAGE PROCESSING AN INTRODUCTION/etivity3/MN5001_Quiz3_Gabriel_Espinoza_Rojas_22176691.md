Consider building an N-gram language model guaranteed to be capable of predicting the correct word (crashed) at the end of this sentence: 
"the computer which I had just put into the machine room on the fifth floor crashed"
, what would be the minimum value of N required to achieve this?




Explain why unigrams (1-gram) are bad at the Shannon Game




Given the raw count tables below, compute the probability of the sentences a and b with and without Add-one (Laplace) smoothing:

a. “i want to want”                      P(a) = ?,	P’(a)=? 
b. “i want to spend”                    P(b) =?,	P’(b)=?

Raw unigram counts:

| i | want | to | eat | chinese | food | lunch | spend |
|---|------|----|-----|---------|------|-------|-------|
| 2533 | 927 | 2417 | 746 | 158 | 1093 | 341 | 278 |

Hint 1: You should infer the value for V using the above table. 

Raw bigram counts:
|         | i | want | to | eat | chinese | food | lunch | spend |
|---------|---|------|----|-----|---------|------|-------|-------|
| i       | 5 | 827 | 0 | 9 | 0 | 0 | 0 | 2 |
| want    | 2 | 0 | 608 | 1 | 6 | 6 | 5 | 1 |
| to      | 2 | 0 | 4 | 686 | 2 | 0 | 6 | 211 |
| eat     | 0 | 0 | 2 | 0 | 16 | 2 | 42 | 0 |
| chinese | 1 | 0 | 0 | 0 | 0 | 82 | 1 | 0 |
| food    | 15 | 0 | 15 | 0 | 1 | 4 | 0 | 0 |
| lunch   | 2 | 0 | 0 | 0 | 0 | 1 | 0 | 0 |
| spend   | 1 | 0 | 1 | 0 | 0 | 0 | 0 | 0 |
Hint 2: You do not need to reconstitute counts in the above tables.


show your work [2 marks]: If you are familiar with LaTeX, this is a good opportunity to use your skills. Latex is a valuable skill to have during your studies and beyond.