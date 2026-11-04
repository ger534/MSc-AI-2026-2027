1. Using an example, explain the difference between users' information needs and queries. [0.5]

The book defines this difference as 
"An *information need* is the topic about which the user desires to know more, and
need is differentiated from a *query*, which is what the user conveys to the comquery puter in an attempt to communicate the information need"

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

Using the boolean matrix:

Row w0 110000
Row w1 110000

Row w5 011111 - complement -> 100000

110000 AND 
110000 AND 
100000 =
100000 

Only doc0 contains w0 and w1, but not w5

5. Generate the Compressed Sparse Row Format (CSR) representation of the matrix below [0.5]

0  0  0
0 "1" 0
0  0 "2" 


CSR uses 3 arrays: Data (or values), Indices (or columns) and Row Pointers

Value (all non-zero elements): ["1" "2"]
Column (this stores all the columns the data/values came from): [1 2]

To understand better the last array, this resource (https://matteding.github.io/2019/04/25/sparse-matrices/) from the complementary material helped me a lot "Adjacent pairs of index pointers determine two things. First, their position in the pointer array is the row number. Second, these values represent the [start:stop] slice of the indices array, and their difference is the NNZ elements in each row. Using the pointers, look up the indices to determine the column for each element in the data." 

In my own words, it starts with zero and then the number of non-zero values per row (NNZ) adds to it until all rows have been accounted for. If the sparse matrix has M rows, indptr is an array containing M+1 elements (https://stackoverflow.com/questions/52299420/scipy-csr-matrix-understand-indptr)

RowPTR : [0 0 1 2]

<!--(accomulative count of non-zero values per row, the last item is the final count)-->

