# rock_paper_scissors
**/ An interactive game of Rock Paper Scissors using computer vision and deep learning. /**

I grew up in the 90's. One of my first game experience was with the Master System II and a little game that came pre-installed. Alex Kidd was afraid of nothing. Except rock, paper and scissors.   

Technology is amazing. While I reminisce hours of games played on a TV that weighted probably more than me, new kids are playing in virtual worlds, without cables. Let's meet in the middle.   

The program I created uses computer vision and deep learning to play a game of rock paper scissors in a live video stream (in this case from a webcam). Sounds impressive… It's not. In fact, it is really simple!

## The workflow   

What do you need to play this game? A hand. And that's it. The program simply needs to recognize the gesture from the hand, compare it against the opponent and output the result (win, loss, draw). 

### 1/ Identifying the hand   

You could come up with a hand tracking algorithm, but I like simplicity. So I created a region of interest which is where the user has to put its hand and do the gesture. It is less flexible and "idiot proof", but it has the merits of simplifying the code.   

We have narrowed down where the action is going to take place. But we still need to "capture the action" (meaning identify the hand). For that, there are several different approaches. The first one that I tried was to use a histogram of oriented gradients but ended up using a simple ''background subtraction''. If you subtract the background of an image you are left with the foreground. And this is what we want here: the hand is (supposed to be) the only thing moving in the region of interest.

### 2/ Recognizing the gesture   

Once we have isolated the hand, we can start thinking of strategies to recognize what gesture it is making. I decided to use deep learning, because it is cool to use deep learning for everything and anything.   

And it is also incredibly easy. Count with me: I recorded a few hundred images of each hand gesture (20 seconds), augmented that dataset (20 seconds) and trained the model (5 minutes). Deep learning in under 6 minutes.     
NB: data augmentation consists of randomly modifying the images I created to create new ones, a little bit different (rotated by some angle, zoomed in or out by some percentage etc.). You can do that directly when training the model but I like to do that separately so a/ I can visualize the modification that I've generated, b/ keep track of the pictures (for reproduction) and c/ memory space was not an issue here. 

### 3/ Output the results    

Once the program has recognized what gesture the person is doing, you just need to implement the rules (paper beats rock, rock beats scissors, scissors beats paper). I hard-coded the logic because it is much simpler. 
Because nobody wanted to play with me, I simulated an opponent. 

## How does it work?  

1/ take the first image as the background (we hypothesize that only the hand will be moving in the region of interest);   

2/ take each frame and subtract the background (this approach also works for diverse skin tone);   

3/ take the result and feed it to the deep learning model in order to identify the gesture;   

4/ compare it to the opponent's gesture according to the rules;    

5/ output the image and result information.   


## How can it be improved?
If that game doesn't get me a job as a developer at Blizzard, I dont know what will! But if I wanted to spend more time and really improve it, I would:   

1/ use a hand tracking system to remove the need of a preset region of interest;   

2/ improve the deep learning model (design, but also training data, including additional hand gestures);   

3/ improve the opponent (either by creating a reinforcement learning agent or by creating more logic like "if player played two X in a row, play Y" - the best strategy is to play randomly, but it is more exciting to build an opponent that seemingly has a strategy that you try to guess);   

4/ improve the graphics and effects of the play screen (count down for each new game, celebratory confetti when winning etc.);    

5/ other ideas you have!
