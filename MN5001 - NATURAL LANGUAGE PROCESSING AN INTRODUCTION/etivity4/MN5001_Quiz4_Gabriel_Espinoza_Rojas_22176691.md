Which type of spelling error is harder to detect, explain why, and use an example to illustrate.

Real-word errors are harder to detect than dictonary mismatches. Unlike non-word errors, cognitive or typograhical errors can hide themselves because the misspelling is part of the dictonary, the known vocabulary. From example, when someone types 'too' instead of 'two' (confusing homophones), that's a cognitive error. I make a lot of typographical errors when I'm texting on a hurry, the auto-correction from my keyboard can change completely the meaning of a sentence if incorrect corrections string along, but at no point there was any words outside the English language. 

Why is the Damerau-Levenshtein distance used for candidate generation in spelling correction?

Remembering concepts learned from previous assignments, Levenshtein uses the deletion, addition and insertation operations to find distances between strings. Damerau-Levenshtein uses also a fourth operation: transpositions. This is a useful addition because the channel that captures the text and the context in which the text is written could lead to mispelling such as "three" instead of "there".


Explain how phonetic algorithms such as Soundex and Metaphone could be used in the candidate selection phase of spelling correction.

During candidate generation, a model can calculate the edit distance to words similar to the spelling of the error (small edit distance to error) or similar to the pronunciation (or both). In this module we used Soundex to learn how names can be spelt quite differently but sound similar due to historical or cultural reasons. The creator of the Methaphone draws a straight comparision (L. Philips. Computer Language Magazine, 7 (12): 39--44  https://archive.org/details/sim_computer-language_1990-12_7_12/page/40/mode/2up?q=metaphone) "Instead of the weird alphanumeric key Soundex gives you, my program constructs a phoneticized and somewhat coded spelling. This has the incidental advantage of making it easier for the programmer to determine what the key represents and whether it's really correct". 

A comparison between the code provided for a word in Philips' article and the function we programmed for E-tivity 2 Task 2.B:
Metaphone: "School" -> SKL
Soundex: "School" -> S400

Regardless, as Jurafsky explains in video 05week_04 State of the Art Systems 7 10 (https://youtu.be/SA_euzCwGwA?list=PLAUFqkTvH_MQ&t=180) that these algorithms convert the misspelling into a representation of their pronunciation. Which, then we can use to draw generate candidates and decise the best fit to correct the mispelling. 


Explain how a classifier can be used to improve the performance of spelling correction.

Two intuitions are required to fully explain this. The language model (or prior) represents how likely is the input word to be a word (using context or not). The channel model (or error model) instead tries to model the noise that created the misspell in the first place. The maximasing product of these two finds the best word to correct the spelling. (Npl - 2.10 - The Noisy Channel Model of Spelling https://youtu.be/jk8jjRZUpf8?t=234)

Classifiers use features to predict their output. The amount of features and their quality depend on how good they capture the real-world signals. In the context of spelling correction, towards the end of video 05week_04 State of the Art Systems 7 10, Jurafsky briefly explains how classifiers not only combinate the output of the channel model (feature 1) and the language model (feature 2), but can use all sorts of extra features to increase their accuracy. He provides a specific example proposing a classifier that predicts the pair ["whether", "weather"], where three extra features are:
- To check for "cloudy" withing +-10 words in the text (Looking for weather-related words)
- Forms of the structure _to VERB_ (Looking for expressions like "whether to go", "wether to say"...)
- If the text following is "or not" (since the expression "weather or not" is common in the English language)

While watching this youtube video I had the auto-generated subtitles turned on and I could see in real time Youtube's text to speech model failing to capture the correct word, confusing "whether" and "weather" multiple times. A classifier with dozens of features to capture differences between this specific pair would have a better accuracy, the more features the better. On top of that, Jurafsky adds that multiple classifiers could be used together to address as many pairs as desired.