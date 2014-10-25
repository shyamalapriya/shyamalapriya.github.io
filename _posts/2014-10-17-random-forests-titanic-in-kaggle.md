---
layout: post
title: "Titanic Survivor Prediction(Kaggle) - Implemented using Random forests"
modified:
categories: 
excerpt:
tags: []
image:
  feature:
date: 2014-10-17T06:46:10-07:00
---

Kaggle put out the Titanic classification problem with a simpler beginner level dataset to try out the Random forest algorithm.

There are a couple of tutorials recommended by Kaggle for this competition and I looked up the one by Trevor Stephens.

It is definitely one of the best-written step-by-step blogs with adequate explanation that I have seen. While I don’t want to repeat the entire [tutorial](trevorstephens.com/post/72916401642/titanic-getting-started-with-r), there were some important lessons from the experience of doing it along with Trevor!

1.	Data exploration (Slicing and dicing data) is an important exercise before jumping into any algorithm implementation. Experiments like predicting everyone dies, or predicting that all females live, trying to see if there were better survival rates if the female were a child. These experiments lets one quickly climb up the leaderboard, without any implementation of any algorithm.
2.	The first implementation of Decision Tree using the default rpart.control which reduces the complexity of the tree built give just a 0.05% improvement but a huge bump in the kaggle leaderboard. What is done next is very interesting! Trevor overrides the defaults of rpart.control and increases the complexity of the decision tree. This results in over fitting of the data and underperformance of the algorithm, i.e., while the model did very well on the training data; it did poorly on the test data.
3.	The Name field appeared to be pretty uninteresting to my untrained eyes. But then, defining additional features like the Title, the Family Id2 based on the Name paved the path for higher accuracy.The data munging that was done here was just amazing. 
	*	First the training and test sets were combined, then string split to derive titles, and some titles combined to make more sense. 
	*	For the Family ID2, adding the family size variable to the id, bucketing the small families (<2 members) etc., curating the data based on certain assumptions.
	*	Finally splitting the training and test sets after the above exercise and re-running the model on the new training set. 
	*	All this didn’t go in vain, the accuracy of the decision tree improved by almost 1%, which was quite significant at this stage of the analysis.
4.	Finally, in order to get to the random forest, remove all the NA’s, blanks from the data, which was skipped until this step. Making intelligent assumptions to remove all the NA data and then building a random forest with 2000 trees, I was sure that this was going to improve accuracy.  Oh Boy! Was I wrong! Sometimes simpler models ARE better than a fancier one. This may just be a one off example, but it was nevertheless an important learning. Trevor did go one step further to try out the conditional inference trees, and got a better result (81% accuracy), than what he first started with during the data exploration stage(75%).  

Overall, while I followed his tutorial in entirety this was an amazing learning not just from a new algorithm perspective, but also about approaching a new problem from the machine learning perspective.
<br>
Fork the code at [Github](https://github.com/shyamalapriya/datashakers-titanic)