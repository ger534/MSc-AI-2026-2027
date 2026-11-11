1. Explain why we use linked lists or variable-length arrays instead of fixed-size arrays for storing inverted indices. [0.5]

This is the first topic disccussed in video 7 3 The Inverted Index 10 42 (https://www.youtube.com/watch?v=Wf6HbY2PQDw). To explain why, first I need to explain what the inverted index is. Professor Manning explains: "for each term (t), we must store a list of all the documents that contain t". Different terms will have different frenquencies, it would be inefficient to pick one size that works for all terms. Moreover, the corpus could later on be modified in such a way that the number of documents where the terms appears increases or reduces, having to then modify the posting lists (the lists of documents in which a particular token occurs) again. 

2. Given the term-document incidence matrix below, 
       a. construct an inverted index in the provided template. [0.5]

corpus = np.array([
     'w0 w1 w2 w3 w4   ', #doc0
     'w0 w1          w5', #doc1
     '      w2       w5', #doc2
     '         w3    w5', #doc3
     '            w4 w5', #doc4
     '               w5', #doc5
 ])

       doc0  doc1  doc2  doc3  doc4  doc5
w0      1     1     0     0     0     0
w1      1     1     0     0     0     0
w2      1     0     1     0     0     0
w3      1     0     0     1     0     0
w4      1     0     0     0     1     0
w5      0     1     1     1     1     1

Template:
{termx, DocumentFrequency} ---> [ docIDn -> docIDn -> . . .]
.
.
.
{w0, 2} ---> [ doc0 -> doc1 ]

{w1, 2} ---> [ doc0 -> doc1 ]

{w2, 2} ---> [ doc0 -> doc2 ]

{w3, 2} ---> [ doc0 -> doc3 ]

{w4, 2} ---> [ doc0 -> doc4 ]

{w5, 5} ---> [ doc1 -> doc2 -> doc3 -> doc4 -> doc5 ]


       b. Apply the merge operation to the inverted matrix from (a) to find the documents that contain w0 and w1, and specify the time complexity of this operation.[0.5]

Video  7 4 Query Processing with the Inverted Index 6 43  (https://youtu.be/5KbynCj7yRQ?t=165) explains this with an example 

{w0, 2} ---> [ doc0 -> doc1 ]

{w1, 2} ---> [ doc0 -> doc1 ]

The two pointers start at 'doc0' for both posting lists and we ask the question "are the two pointers pointing at the same document ID?", and the answer is yes so we add 'doc0' to the result list [ doc0 ]

And both pointers advance one position and the question is asked again. The answer is yes again, so 'doc1' is added to the result list  [ doc0, doc1 ]

At this point both lists are exhausted so the merge is completed. 

About the complexity, Professor Manning explains: "if the list lengths are x and y, the merge takes O(x+y) operations" and also says that it is crucial that the postings are sorted by docID to keep this complexity linear, otherwise complexity would be O(N^2)

So the complexity of the merge between w0 and w1 is

$ O(x+y) = O(2+2) = O(4) $

3. Why do we commonly store the vocabulary in memory but the postings on disk [0.5]  

<!--Posting lists -> the list of documents in which a particular token occurs. (sorted by document id)-->

Video 7 3 The Inverted Index 10 42 (https://www.youtube.com/watch?v=Wf6HbY2PQDw) goes over this.

<!--Section 'where do we pay in storage?' -> The size of the vocabulary (referred in the video as 'terms and counts') is considered relatively modest (500,000 in the example). And the posting lists, considering documents of 1000 words, is less than a billion -->

See book:

Let us now consider a more realistic scenario, simultaneously using the
opportunity to introduce some terminology and notation. Suppose we have
N = 1 million documents. By documents we mean whatever units we have
decided to build a retrieval system over. They might be individual memos
or chapters of a book (see Section 2.1.2 (page 20) for further discussion). 
We refer to the group of documents over which we perform retrieval as 
the (document) collection. It is sometimes also referred to as a corpus (a body of texts).
Suppose each document is about 1,000 words long (2–3 book pages). If we
assume an average of 6 bytes per word including spaces and punctuation,
then this is a document collection about 6 gigabytes (GB) in size. Typically,
there might be about M = 500,000 distinct terms in these documents. 


4. What are the common preprocessing steps in creating an inverted index, and what is their impact on the search results [1]


Recall the major steps in inverted index construction:
1. Collect the documents to be indexed.
2. Tokenize the text.
3. Do linguistic preprocessing of tokens.
4. Index the documents that each term occurs in.



The book defines the four following stages for determining the vocabulary of terms (titled 'initial stages of text processing' in video 7 3 The Inverted Index 10 42 https://www.youtube.com/watch?v=Wf6HbY2PQDw):

2.2.1 Tokenization
Given a character sequence and a defined document unit, tokenization is the task of chopping it up into pieces, called tokens, perhaps at the same time
throwing away certain characters, such as punctuation (i.e. "John's")

2.2.3 Normalization (equivalence classing of terms)
the process of canonicalizing tokens so that matches occur despite superficial differences in the character sequences of the tokens. (i.e. "USA" = "U.S.A.")

2.2.4 Stemming and lemmatization (lemmatization is omitted in the video)
Stemming usually refers to a crude heuristic process that chops off the ends of words in the hope of achieving this goal correctly most of the time, and often includes the removal of derivational affixes

Lemmatization usually refers to doing things properly with the use of a vocabulary and morphological analysis of words, normally aiming to remove inflectional endings only and to return the base or dictionary form of a word, which is known as the lemma.

2.2.2 Dropping common terms: stop words
Very common words can be omitted entirely (i.e. "the", "of", "a")

About the stop words, Professor Manning mentions in the video that wi