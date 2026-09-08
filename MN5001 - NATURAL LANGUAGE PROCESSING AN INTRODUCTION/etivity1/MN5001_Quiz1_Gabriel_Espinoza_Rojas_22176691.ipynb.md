1. Using an example, explain the difference between Type I and Type II Errors in the context of Regular expressions.

(https://www.youtube.com/watch?v=808M7q8QX0E&t=626s)
False positives - Type I - matching strings that should not match
False negative - Type II - not matching strings that should match

2. How do false positives and false negatives affect precision and recall

Minimising false positives increases precision (also called precision)
Minimising false negatives increases recall (also called coverage)

3. Count the number of Types and Tokens in this sentence: “NLP is the art of analysing and understanding human languages by machines.”

Professor Dan Jurafsky says that it is always important to explain our goals behind your counting. (https://www.youtube.com/watch?v=xsIDTmo1NOg&list=PLAUFqkTvH_MQ&index=3)

Normalising the multiword expression 'NLP' as 'Natural Language Processing', the sentence has

Tokens (every word form): 14

Types (lemmas): 13

because language = languages = same stem/lemma. 


4. Write a sample sentence containing a Fragment and a filled pause.

A sentence with both disfluencies: "I do uh main- mainly business data processing"

disfluency This utterance has two kinds of disfluencies. The broken-off word, where 'main-' is the fragment and 'uh'/'um' is the filler or filled pause. (chapter 2, section 2.1 of the book)


5. Explain the difference between lemmatisation and stemming, and provide an example for each. 

Lemmatisation is the mapping of each token to a true morphological lemma, meaning, the linguistic root. Stemming is a simplified version of lemmatisation that consists in crudely chopping off thew affixes a token might have

<!--I would describe lemmas like rules we can set up. For example NLP = Natural Language processing. Or counting the expression l' as the token 'le' in a French context. Stemming is detecting the token's root, to identify whether a token is a new vocabulary type or just an expression of an already known type.-->

6. Explain overstemming and understemming errors with the help of an example.

Overstemming would be 'chopping' more than necessary, for example a rule to remove all 's' characters (to leave cats = cat = same lemma), could also take the 's' characters from words such as 'was' (turning to 'wa') or this (turning to 'thi'). The opposite case would be 



