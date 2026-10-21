1. With the help of an example explain why accuracy is not a good measure of text classification systems’ performance. [0.5 mark]

https://youtu.be/mjOgb4T7yyo?list=PLAUFqkTvH_MQ&t=16 

You man has the shoe example. 

The book invites the reader to think of self as the CEO of the company 'Delicious Pie', and presents the following problem: "you need to know
what people are saying about your pies on social media, so you build a system that detects tweets concerning Delicious Pie. Here the positive class is tweets about Delicious Pie and the negative class is all other tweets". The problem with accuracy here is that the inbalance between tweets that are actually about Delicious Pie would be practically zero in comparison with all the other tweets. The book concludes "accuracy is not a good metric when the goal is to discover something that is rare, or at least not completely balanced in frequency, which is a very common situation in the world". Otherwise you'll end up with a nothing pie.

2. Compute the arithmetic, geometric, and harmonic means of 10 and 100. Show your work with the help of Latex. [0.5 mark]

Harmonic mean is the F measure (F1 is when it is balanced)
https://youtu.be/mjOgb4T7yyo?list=PLAUFqkTvH_MQ&t=667

https://machinelearningmastery.com/arithmetic-geometric-and-harmonic-means-for-machine-learning/



3. Given the two confusion tables below, compute [1.5 marks]
a. Microaveraged precision, recall, and F1 
b. Macroaveraged precision, recall, and F1
c. Explain the reason for the difference between the obtained Microaveraged and Macroaveraged F1 measures. 
Show your work with the help of Latex.
Round all numbers to 3 decimal points. 

Class Food 
|                 | Truth: YES | Truth: NO |
| Classifier: YES | 800        |  200      |
| Classifier: NO  | 200        |  500      |


Class Drink
|                 | Truth: YES | Truth: NO |
| Classifier: YES | 70        |  30        |
| Classifier: NO  | 3         |  100       |


Video https://youtu.be/NjhVTN19JDI?list=PLAUFqkTvH_MQ&t=215 talks about a) and b)



4. List the benefits of using k-fold cross-validation and explain how k-fold cross-validation could be done, 
where:
k = 10, and there are a total of 120 documents in our dataset. [0.5 mark]


