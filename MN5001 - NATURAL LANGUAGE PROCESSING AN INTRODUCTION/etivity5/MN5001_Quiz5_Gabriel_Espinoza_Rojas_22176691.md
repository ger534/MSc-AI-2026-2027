<b>1. With the help of an example explain why the Multinomial Naive Bayes Independent assumptions are incorrect.</b>

<!-- There are TWO assumptions to cover, not one:

     (a) BAG OF WORDS - position doesn't matter. P(w|c) is the same whether the
         word appears first or last.
     (b) CONDITIONAL INDEPENDENCE - P(w1, w2, ..., wn | c) = P(w1|c) * P(w2|c) * ...
         i.e. every word is independent of every other, given the class.

     Both are plainly false about language. Pick an example that breaks them:
       - word order: "the dog bit the man" vs "the man bit the dog" - identical BoW
       - dependence: in a GB document, seeing "London" makes "England" far more
         likely than its standalone rate; the model treats them as unrelated
       - collocations / n-grams generally: "New York", "not good"
       - NEGATION is the sharpest one for sentiment: "not good" - BoW sees "good"

     Then the punchline Jurafsky makes: despite the assumptions being wrong,
     Naive Bayes works well in practice for classification, because it only needs
     the ARGMAX to be right, not the probabilities themselves. -->



<b>2. Select the most appropriate stop words to be removed from the two bags of words (a.k.a word clouds) shown below; one per cloud. Words' font sizes are proportional to their frequency in the corpus.</b>

<!-- One word per cloud.

     Cloud 2 (already stop-word filtered): content words only - climate, change,
     global, warming, level, report, emissions, protocol, agreement... is the right answer about a word that is uninformative *for this corpus* rather than uninformative in general?

     Justify the choice: highest frequency + lowest discriminative value. Tie it to
     feature selection - a term appearing in every document carries no information
     for distinguishing between documents. -->

The clouds are another representation of that Dan calls bags of words.

From cloud 1 I think 'the' is the obvious answer. It takes a lot of space and adds nothing to the cloud. 
For cloud 2, because they are no stop words (https://youtu.be/Ge612JZGBMU?t=308) the matter becomes about the word that adds the least amount of information to the cloud. In this context, I believe it is: XXXX. 


<b>3. Given the four training documents in the table below, infer the class of the test document (doc #5). Show your work, i.e. computations of priors and conditional probabilities. [2 marks]</b>

Training:
| Doc | Words | Class |
|-----|-------|-------|
| 1 | London is the Capital of GB | GB |
| 2 | Oxford is a city in GB | GB |
| 3 | Dublin is the capital of Ireland | IE |
| 4 | Limerick is a city in Ireland | IE |

Test:
| Doc | Words | Class |
|-----|-------|-------|
| 5 | University of Limerick Wolves | ? |

<!-- NOTE: doc #5 here is "University of Limerick WOLVES" - one word longer than the E-tivity's test doc. Check which words are in the vocabulary.

     MEGA-DOCUMENTS (lowercase, concatenated per class)
       GB: london is the capital of gb oxford is a city in gb
       IE: dublin is the capital of ireland limerick is a city in ireland

     VOCABULARY
       V = distinct words across BOTH classes;  |V| = ?

     CONDITIONALS with add-one smoothing
       P(w|c) = (count(w,c) + 1) / (total words in class c + |V|)
       - denominator is TOTAL TOKENS in the class, not distinct words
       - compute one line per word of doc 5 that is in V
       - decide and STATE what you do with out-of-vocabulary words
         (the usual convention: drop them, since they contribute the same
         factor to both classes and cannot change the argmax)

     CHOOSING A CLASS
       P(IE|d5) ∝ P(IE) * prod P(w|IE)
       P(GB|d5) ∝ P(GB) * prod P(w|GB)
       argmax -> inferred class -->

**Priors:**
How many times does the class GB ocurrs in our training set out of the how many total documents are there in our training set?

$$P(GB) = \frac{2}{4} = 0.5 $$

How many times does the class IE ocurrs in our training set out of the how many total documents are there in our training set?
$$P(IE) = \frac{2}{4} = 0.5 $$

Considering what Jurafsky says about unknown words (words not present in the training docs), I'll remove the words University and Wolves https://youtu.be/Ge612JZGBMU?t=268

**Conditional probabilities:**

How many times is each word given each class in our training data. 

V = { London, is, the, Capital, of, GB, Oxford, a, city, in, Dublin, capital, Ireland, Limerick } [14]

Taking Capital as equal to capital V = 13

Building those mega-document Jurafsky mentions (https://youtu.be/Ge612JZGBMU?t=64)

count(GB) = 12 [london is the capital of gb oxford is a city in GB]

count(IE) = 12 [dublin is the capital of ireland limerick is a city in ireland]

$$P(w_i|c) = \frac{count(w_i, c) + 1}{count(c) + |V|}$$

Class GB:


<!--$$P(University | GB) = \frac{count(University, GB) + 1}{count(GB) + |V|} = \frac{0 + 1}{12 + 13} = \frac{0 + 1}{12 + 13} = \frac{1}{25} = 0.04$$-->

$$ P(of | GB) =  \frac{count(of, GB) + 1}{count(GB) + |V|} = \frac{1 + 1}{12 + 13} = \frac{1 + 1}{12 + 13} = \frac{2}{25} = 0.08$$

$$ P(Limerick | GB) = \frac{count(Limerick, GB) + 1}{count(GB) + |V|} = \frac{0 + 1}{12 + 13} = \frac{0 + 1}{12 + 13} = \frac{1}{25} = 0.04$$

<!--$$ P(Wolves | GB) = \frac{count(Wolves, GB) + 1}{count(GB) + |V|} = \frac{0 + 1}{12 + 13} = \frac{0 + 1}{12 + 13} = \frac{1}{25} = 0.04$$-->

Class IE:

<!--$$ P(University | IE) = \frac{count(University, IE) + 1}{count(IE) + |V|} = \frac{0 + 1}{12 + 13} = \frac{0 + 1}{12 + 13} = \frac{1}{25} = 0.04 $$-->

$$ P(of | IE) = \frac{count(of, IE) + 1}{count(IE) + |V|} = \frac{1 + 1}{12 + 13} = \frac{1 + 1}{12 + 13} = \frac{2}{25} = 0.08$$

$$ P(Limerick | IE) = \frac{count(Limerick, IE) + 1}{count(IE) + |V|} = \frac{1 + 1}{12 + 13} = \frac{1 + 1}{12 + 13} = \frac{2}{25} = 0.08$$

<!--$$ P(Wolves | IE) = \frac{count(Wolves, IE) + 1}{count(IE) + |V|} = \frac{0 + 1}{12 + 13} = \frac{0 + 1}{12 + 13} = \frac{1}{25} = 0.04$$-->


**Choosing a class:**

Now we use the priors and likehoods to compute the probability of the test sentence being of class GB or IE.

$$P(GB|d5) \propto \frac{2}{4} * \frac{2}{25} * \frac{1}{25} = 0.0016 $$

$$P(IE|d5) \propto \frac{2}{4} * \frac{2}{25} * \frac{2}{25} = 0.0032 $$

<!--The ∝ matters: these are unnormalised scores, not probabilities, because the P(d) denominator is dropped-->

**Inferred class:**

Since
$$P(IE|d5) > P(GB|d5)$$
the inferred class is IE.


