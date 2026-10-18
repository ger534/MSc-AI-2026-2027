<b>1. With the help of an example explain why the Multinomial Naive Bayes Independent assumptions are incorrect.</b>

The first assumption is about the concept around the input data ('Bag of Words'). The BoW by nature leaves no context from the original text. Relationships arise from frequency (unigrams). The probability of each class/sentiment/category is calculated with a unigram. "man bit dog" and "dog bit man" have the exact BoW representation, but it is evident these two sentences are very different. Assuming that position does not matter is incorrect.

A second assumption to make the computation more possible is to ignore the relationships other words would have with one another in a specific document given a class. The simplification here is to treat every word independent from one another. Not the same as the Markov assumption but similar. For my own sanity, I wanted to review what the difference was. 

In lesson 3 we had to calculate sentence probability with a 2-gram, assuming:
$$P(not\ good) = P(not|<s>) * P(good|not) * P(</s>|good)$$

And this is just one interpretation, the Markov assumption was about truncating the original text to different degrees (N-grams), trying to leave some of the context. But the independence assumption the multinomial NB makes words conditional to the class only:
$$P(not\ good | c) =  P(not | c) * P(good | c)$$

In this example, the classifier counts "not" and "good" as two independent pieces of evidence but in reality, they are strongly dependent, "not good" is clearly negative, but the classifier (with classes 'negative' and 'positive') will more likely account for 'good' as a positive element when doing $P(good | positive)$.

However, multinomial Naive Bayes classifier turns out not to be so naive (Jurafsky mentions). Despite making incorrect assumptions, the classifier only needs the correct class to have the highest score.
 

<b>2. Select the most appropriate stop words to be removed, from the two bags of words (a.k.a word clouds) shown below; one per cloud. Words' font sizes are proportional to their frequency in the corpus.</b>

The clouds are another representation of what Dan calls bags of words. The Appendix B: Naive Bayes Classification (https://web.stanford.edu/~jurafsky/slp3/B.pdf), defines stop words as "a class of words that some systems decide to completely ignore". He adds that they are "very frequent words like 'the' and 'a'" and explains that a way they can be selected is "by sorting the vocabulary by frequency in the training set, and defining the top 10–100 vocabulary entries as stop words".

Using this definition, from cloud 1: 'the' is the obvious answer. For cloud 2, because the stop words have already been removed I believe the matter becomes about the word that adds the least amount of information to the cloud. In this context, I would choose 'report'. However, if the same rule described in the book was applied, the procedure would pick the word 'climate'.

One last important note is that Jurafsky closes the explanation of stop words with  "In most text classification applications, however, using a stop word list doesn’t improve performance, and so it is more common to make use of the entire vocabulary and not use a stop word list".  (https://youtu.be/Ge612JZGBMU?t=308)

<b>3. Given the four training documents in the table below, infer the class of the test document (doc #5). Show your work, i.e. computations of priors and conditional probabilities. [2 marks]</b>

**Priors:**
How many times does the class GB occurs in our training set out of the how many total documents are there in our training set?

$$P(GB) = \frac{2}{4} = 0.5 $$

How many times does the class IE occurs in our training set out of the how many total documents are there in our training set?
$$P(IE) = \frac{2}{4} = 0.5 $$

Considering what Jurafsky says about unknown words (words not present in the training docs), I'll remove the words University and Wolves https://youtu.be/Ge612JZGBMU?t=268

**Conditional probabilities:**

How many times is each word given each class in our training data. 

V = { London, is, the, Capital, of, GB, Oxford, a, city, in, Dublin, capital, Ireland, Limerick } [14]

Taking 'Capital' as equal to 'capital' V = 13 (normalisation of the text).

Building those mega-documents Jurafsky mentions (https://youtu.be/Ge612JZGBMU?t=64)

count(GB) = 12 [london is the capital of gb oxford is a city in GB]

count(IE) = 12 [dublin is the capital of ireland limerick is a city in ireland]

$$P(w_i|c) = \frac{count(w_i, c) + 1}{count(c) + |V|}$$

Class GB:


<!--$$P(University | GB) = \frac{count(University, GB) + 1}{count(GB) + |V|} = \frac{0 + 1}{12 + 13} = \frac{0 + 1}{12 + 13} = \frac{1}{25} = 0.04$$-->

$$ P(of | GB) =  \frac{count(of, GB) + 1}{count(GB) + |V|} = \frac{1 + 1}{12 + 13} = \frac{2}{25} = 0.08$$

$$ P(Limerick | GB) = \frac{count(Limerick, GB) + 1}{count(GB) + |V|} = \frac{0 + 1}{12 + 13} = \frac{1}{25} = 0.04$$

Class IE:

$$ P(of | IE) = \frac{count(of, IE) + 1}{count(IE) + |V|} = \frac{1 + 1}{12 + 13} = \frac{2}{25} = 0.08$$

$$ P(Limerick | IE) = \frac{count(Limerick, IE) + 1}{count(IE) + |V|} = \frac{1 + 1}{12 + 13} = \frac{2}{25} = 0.08$$


**Choosing a class:**

Now we use the priors and likelihoods to compute the probability of the test sentence being of class GB or IE.

$$P(GB|d5) \propto \frac{2}{4} * \frac{2}{25} * \frac{1}{25} \propto 0.0016 $$

$$P(IE|d5) \propto \frac{2}{4} * \frac{2}{25} * \frac{2}{25} \propto 0.0032 $$

<!--The ∝ matters: these are unnormalised scores, not probabilities, because the P(d) denominator is dropped-->

**Inferred class:**

Since
$$P(IE|d5) > P(GB|d5)$$
the inferred class is IE.


