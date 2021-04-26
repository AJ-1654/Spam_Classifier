# <center>**Email Classification**</center>

  

In the first part of the project we have implemented the spam classifier using the <em><strong>Naive Bayes</strong></em> classifier from scratch. `Our objective was to understand the functioning of naive bayes classifier in the classification of emails throughly.`

  

In the second part of the project we have implemented the spam classifier using naive bayes classifier from the scikit learn library.

  
  

We have collected the data set from [SpamAssassin public mail corpus](https://spamassassin.apache.org/old/publiccorpus/) containing around 1900 spam emails and 3900 legit emails.

  
  

## <strong>Spam classification using Naive Bayes</strong>

  

### **Architecture of spam classifier**

An Email body is divided into three parts header, subject line and body where header contains the information of the sender, subject contains the subject of the email and body contains the actual content of the email. Before the email can be classified by a filter, preprocessing of the email is required to get the desired features.

  
  

> Preprocessing the Emails

1. The body of the emails are extracted from the email.
2. A pandas data frame is created having the email bodies and category.
3. Morphological analysis of the messages in the data set is done. After the morphological analysis each message body is converted into the individual words. We have used the natural language tool kit (nltk) for this purpose. It involves:<br>
	- Removing the HTML Tags from the body of the email.
	- Stemming of the words.
	- Removal of stop words.
4. A pandas series is created having all the words in all the emails.
5. A vocabulary is created with the most frequent 2500 words.
6. A feature matrix is created having entry for each word in the email.
7. Data is split into 70% training and 30% test set.
8. A sparse matrix is created for the training and the testing data.
	
---	
### Bayes Theorem

<img src="https://render.githubusercontent.com/render/math?math=P(A \, | \, B) = \frac{P(B \, | \, A) \, P(A)} {P(B)} = -1">
We assume that each word in an email is independent of every other word an hence the name <em>Naive Bayes</em>.

If a word is present in an email we can write the probability of the email being spam given that it contains a particular word as:
<img src="https://render.githubusercontent.com/render/math?math=$P(spam \, | \, word) = \frac{P(word \, | \, spam) \, P(spam)} {P(word)}$">
and the email being ham as:
<img src="https://render.githubusercontent.com/render/math?math=$P(ham \, | \, word) = \frac{P(word \, | \, ham) \, P(ham)} {P(word)}$">

For all the words in our vocabulary, we will find <img src="https://render.githubusercontent.com/render/math?math=$P(word)$"> , the probability of a given word and <img src="https://render.githubusercontent.com/render/math?math=$P(word \,|\, Spam)$"> 
, the probability of the word in spam emails.
We will also calculate the probability of spam emails in training data as as:
<img src="https://render.githubusercontent.com/render/math?math=$ P(spam) = \frac{number\,of\,spam\,emails}{total\,number\,of \,emails}$">

> Training the Naive Bayes Classifier

1. Calculate <img src="https://render.githubusercontent.com/render/math?math=$P(spam)$">, the probability of spam emails.
2. For all the words in the dictionary calculate<br>
  - <img src="https://render.githubusercontent.com/render/math?math=P(ham \, | \, word)">
  - <img src="https://render.githubusercontent.com/render/math?math=P(spam \, | \, word)">

---
Let's say an email contains words X and Y. 
The probability of the email being spam is:
<img src="https://render.githubusercontent.com/render/math?math=P(spam\,|X,\,Y)=\frac{P(X\,|\,spam)}{P(X)}*\frac{P(Y\,|\,spam)}{P(Y)}*P(spam)">

The probability of the email being ham is:
<img src="https://render.githubusercontent.com/render/math?math=P(ham\,|X,\,Y)=\frac{P(X\,|\,ham)}{P(X)}*\frac{P(Y\,|\,ham)}{P(Y)}*P(ham)">

For prediction we can remove the term <img src="https://render.githubusercontent.com/render/math?math=$P(word)$"> from the denominator of our expression because it is common in both cases. 

If <img src="https://render.githubusercontent.com/render/math?math=P(spam\,|X,\,Y) > P(ham\,|X,\,Y)"> then the email will be classified as spam else it will be classified as non-spam or ham.

> Testing the Naive Bayes Classifier
1.	Set the Priori as <img src="https://render.githubusercontent.com/render/math?math=$P(spam)$">
2.	Calculate the probability of an email being spam and non-spam by taking product of the test data and probabilities of individual words and multiply the priori to the result.
3.	An email will be classified comparing the two probabilities.
---
>Results

   <center>Confusion Matrix for 1722 emails in test set</center> <br/><br/>

<center>
<table>
<tr>
<td>
<td><strong>Predicted Spam</strong></td>
<td><strong>Predicted Ham</strong></td>
</tr>
<tr>
<td><strong>Spam</strong></td>
<td> True Positives = 557 </td>
<td>False Negatives = 30</td>
</tr>
<tr>
<td><strong>Ham</strong></td>
<td>False Positives = 15</td>
<td>True Negatives = 1120</td>
</tr>





</table>

</center>




-	**Accuracy** = <img src="https://render.githubusercontent.com/render/math?math=$\frac{emails\,classified\,correctly}{total\,number\,of\,emails}$"> = 97.39% 
-	**Recall score** = <img src="https://render.githubusercontent.com/render/math?math=$\frac{True\,Positives}{True\,Posotives\,+\,False\,Negatives}$"> = 94.89%
-	**Precision score** = <img src="https://render.githubusercontent.com/render/math?math=$\frac{True\,Positives}{True\,Posotives\,+\,False\,Positives}$"> = 97.37%
-	**F score** = <img src="https://render.githubusercontent.com/render/math?math=$2*\frac{Precision\,*\,Recall}{Precision\,+\,Recall}$"> = 96%


<br><br>


## <strong>Spam classification using scikit learn</strong>
Implementation of spam classifier using the naive bayes classifier from the scikit learn library.
The vocabulary was generated using <em>CountVectorizer</em> from the sklearn library instead of generating the features manually.
>Results

- **Accuracy** <img src="https://render.githubusercontent.com/render/math?math=\,:\,93.61">
- **Recall** <img src="https://render.githubusercontent.com/render/math?math=\,:\,80.68">
- **Precision** <img src="https://render.githubusercontent.com/render/math?math=\,:\,99.11">
- **F1 score** <img src="https://render.githubusercontent.com/render/math?math=\,:\,88.95">

