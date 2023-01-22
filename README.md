CSE 258 Assignment 1: 

1- Read prediction:

I first based myself off my answers in homework3, where I tried 
different techniques. In that homework, I first did that using most popular books, and tuned this 
parameter in order to achieve the highest accuracy (which was about 74%). And I realized that 
after including Jaccard Similarity, my accuracy was dropping (which  was weird) but the professor
explained it as part of the erroneous data that was given to us. And even after tuning jaccard, i still
weren't able to surpass my previous scores that only utilized Most Popular Books approach. 
When I started this assignment, I ran again the previous models just to check that I wasn't doing anything
wrong, and I realized that my answers matched those of Hw3. So instead I reverted to other data
manipulation. I first tried to make use of the rating prediction model that was actually working well for me (will 
discuss in details later), and put cutoffs on if the expected rating of the user is above a certain threshold
(I tried 2, 3, 4 and stuff in between), make the read predicition 1, but it performed horribly on the data. 
I also tried to take advatange of the professor's book (personalized machine learning), I tried different models 
that are listed there (surprise, BPR and many more) but still it was only performing better than the naive predictor
(just above 0.5). Sir had given us a hint, that the data was made just like we made validation set before (adding negative interactions)
which makes each user have at most half of data as read and half as not so I tried exploting that.
It performed better than before but was still bad (even after trying Jaccard, Cosine and Pearons's similarities and 
even a mix of these). So i knew I had to change it. 

The last thing i tried(which worked) is I figured out that was wrong with the data is actually not having enough meaningful data, ie
 no overlap where the model can actually learn smilarity so I had to create it manually. what i did is, i created two big sets,
one taking all the items of all the users that ever interacted with the item in question, all the items of all the users of all the items
interacted by the user in question. This model performed really well, I dont know if because I am creating this artifical overlap that
should have been there already, or is it only because of this dataset, but I decided to keep it. 
After gathering these two  datasets, I would do a jaccard similarity on them, sort them by reverse order, and pick the top half to be 1
and the bottom half to be 0. 





2 - Rating prediction:

For rating prediciton, I used the model that I used in HW3 just with a bit of number manipulation.
I just first tried the rating prediction model, which was there on the slides, that used alpha beta user and beta 
item to make the rating prediction. I tuned in the most popular books model and got a best threshold of 74% so i just
used it and I also tuned lambda to get the best alpha which i directly used and it gave a really good score.

What i did to increase the score is basically number manipulation, in a sense where I clipped all ratings above 5
and all ratings less than 0. then i tried different rounding techniques, then i discovered that rounding 0.1 
is the best (so a 2.9 will become a 3 and a 1.1 will become a 1). I also tried rounding other numbers,
and I realized that 3 is the actually most common rating so i rounded everything that was in the range of 2.7 to 3.3
to a rating of 3 which is the only thing that increased the MSE. I dont know if that overfitted the model, but i think 
its just how the data is repartioned. 



