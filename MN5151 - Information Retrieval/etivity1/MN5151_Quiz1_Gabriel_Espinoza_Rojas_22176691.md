1. Using an example, explain the difference between users' information needs and queries. [0.5]



2. With the help of an example, show how query formulation could affect Precision and Recall. [0.5]



3. What are the shortcomings of linear search via the Grep command for information retrieval? [0.5]

https://youtu.be/e81nC0LO0A8

It is slow for large corpora. It does not handle well negative expression (e.g. find documents that NOT contain a specific word) and other operations such as relationships (e.g. find the word Romans near countrymen). But moreover, the linear scan for matching can't do ranked retrieval (finding the best documents to return for a query).


4. Given the term-document incidence matrix below, find the documents that contain w0 and w1, but not w5. Show your work. [1]

       doc0  doc1  doc2  doc3  doc4  doc5
w0      1     1     0     0     0     0
w1      1     1     0     0     0     0
w2      1     0     1     0     0     0
w3      1     0     0     1     0     0
w4      1     0     0     0     1     0
w5      0     1     1     1     1     1



5. Generate the Compressed Sparse Row Format (CSR) representation of the matrix below [0.5]

0 0 0
0 1 0
0 0 2 


