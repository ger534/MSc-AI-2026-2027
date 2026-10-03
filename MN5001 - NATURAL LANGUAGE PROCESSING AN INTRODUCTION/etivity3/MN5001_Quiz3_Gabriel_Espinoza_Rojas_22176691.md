<strong>Consider building an N-gram language model guaranteed to be capable of predicting the correct word (crashed) at the end of this sentence: 
"the computer which I had just put into the machine room on the fifth floor crashed"
, what would be the minimum value of N required to achieve this?</strong>

This sentence is used by professor Jurafsky in video https://youtu.be/hM49MPmakNI?t=466. By using the N-gram language model, he says that we would need to know the subject of the sentence (computer), that requires a distance of N=15.


<strong>Explain why unigrams (1-gram) are bad at the Shannon Game</strong>

The Shannon game consists in guessing the next word in a sentence (https://youtu.be/B_2bntDYano?t=184). Because the 1-grams or unigrams don't look at any previous words in the sentence to assign probabilities, they are highly unlikely to predict correctly the next word by just looking at the frequency of one word. Mathematically:

$$P(w_i) = \frac{count(w_i)}{N}$$

In any other N-gram, the denominator for the probability would carry context from previous words (or word in the case of 2-grams), but N in this case is just the total number of words in the corpus. 

One example Jurafsky uses is "The 33rd President of the US was ______". With the proper amount of context, the right answer becomes trivial, without it, almost impossible. 

The Shannon Game is an intuition of perplexity, a good model will guess correctly, a bad model won't. Unigrams have the highest perplexity. "A trigram model is less surprised than a unigram model because it has a better idea of what words might come next, and so it assigns them a higher probability." (Chapter 3 book, p.10)


Given the raw count tables below, compute the probability of the sentences a and b with and without Add-one (Laplace) smoothing:

a. “i want to want”                      P(a) = ?,	P’(a)=? 
b. “i want to spend”                    P(b) =?,	P’(b)=?

$$P(w_{i}|w_{i-1}) = \frac{c(w_{i-1}, w_{i})} {c(w_{i-1})} $$


a. “i want to want” 

$$P(i\ want\ to\ want) = ? $$

With the chain rule and the Markov assumption, we can say that:

$$P(i\ want\ to\ want) = P(want|i) * P(to|want) * P(want|to)$$

Note: I was unsure to whether I needed to acknowledge the tokens that usually mark the start or end of a sentence (`<s>`, `</s>`). I asked a question about this in the forum and the professor clarified: 'There is nothing special about the <s> and </s> tokens. We treat them like any other token, i.e. there is no need to compute their probability if they do not appear in the string'.

Let's calculate each individually: 
$$P(w_i | w_{i-1}) = \frac{count(w_{i-1}, w_i)}{count(w_{i-1})}$$

$$ P(want|i) =  \frac{count(i, want)}{count(i)} = \frac{827}{2533} = 0.3265 $$
$$ P(to|want) =  \frac{count(want, to)}{count(want)} = \frac{608}{927} = 0.6559 $$
$$ P(want|to) =  \frac{count(to, want)}{count(to)} = \frac{0}{2417} = 0 $$

$$P(i\ want\ to\ want) = 0.3265 * 0.6559 * 0 = 0 $$

Now using add-one smoothing or Laplace smoothing

$$P'(i\ want\ to\ want) = ? $$

$$P(w_i | w_{i-1}) = \frac{count(w_{i-1}, w_i) + 1}{count(w_{i-1})+V}$$

`V = 8` (counting the columns of the unigram table)

$$ P(want|i) =  \frac{count(i, want) + 1}{count(i) + 8} = \frac{828}{2541} = 0.3259 $$
$$ P(to|want) =  \frac{count(want, to) + 1}{count(want) + 8} = \frac{609}{935} = 0.6513 $$
$$ P(want|to) =  \frac{count(to, want) + 1}{count(to) + 8} = \frac{1}{2425} = 0.0004 $$

$$ P'(i\ want\ to\ want) = 0.3259 * 0.6513 * 0.000412 \approx 8.57 \times 10^{-5}$$


b. “i want to spend” 

$$P(i\ want\ to\ spend) = ? $$

$$P(i\ want\ to\ spend) = P(want|i) * P(to|want) * P(spend|to)$$

Let's calculate each individually: 
$$P(w_i | w_{i-1}) = \frac{count(w_{i-1}, w_i)}{count(w_{i-1})}$$

$$ P(want|i) =  \frac{count(i, want)}{count(i)} = \frac{827}{2533} = 0.3265 $$
$$ P(to|want) =  \frac{count(want, to)}{count(want)} = \frac{608}{927} = 0.6559 $$
$$ P(spend|to) =  \frac{count(to, spend)}{count(to)} = \frac{211}{2417} = 0.0873 $$

$$P(i\ want\ to\ spend) = 0.3265 * 0.6559 * 0.0873 = 0.0187 $$



Now using add-one smoothing or Laplace smoothing

$$P'(i\ want\ to\ spend) = ? $$

$$P(w_i | w_{i-1}) = \frac{count(w_{i-1}, w_i) + 1}{count(w_{i-1})+V}$$

`V = 8` (counting the columns of the unigram table)

$$ P(want|i) =  \frac{count(i, want) + 1}{count(i) + 8} = \frac{828}{2541} = 0.3259 $$
$$ P(to|want) =  \frac{count(want, to) + 1}{count(want) + 8} = \frac{609}{935} = 0.6513 $$
$$ P(spend|to) =  \frac{count(to, spend) + 1}{count(to) + 8} = \frac{212}{2425} = 0.0874 $$

$$ P'(i\ want\ to\ spend) = 0.3259 * 0.6513 * 0.0874 \approx 0.0185 $$
