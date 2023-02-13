
#Objective
Jackpot! You've landed a summer gig in Las Vegas! Unfortunately, its 2021, and the casinos are closed  due to COVID-19. Your boss wants to move some of the business online and asks you to build an app — a simple slot machine game, with a little twist. Build it to ensure that the house always wins!
##Brief
When a player starts a game, they are allocated 10 credits.  
Pulling the machine lever (rolling the slots) costs 1 credit.  
The game screen has 1 row with 3 blocks.  
For player to win the roll, they have to get the same symbol in each block.
There are 4 possible symbols: cherry (10 credits reward), lemon (20 credits reward), orange (30 credits  reward), and watermelon (40 credits reward).
If the player keeps winning, they can play forever, but the house has something to say about that... There is CASH OUT button on the screen, but there's a twist there as well.

##Tasks
• Implement assignment using:
o Language: Javascript
o Framework: Vue 2 or 3
• When a user opens the app (Browser), they have 10 starting credits.
• Client side: (Logic of the game):
o implement a function to do the following:
▪ When a user has less than 40 credits in the game, their rolls are truly random. • If a user has between 40 and 60 credits, then we begin to slightly cheat:
o For each winning roll, before sending back the result, function  
does one 30% chance roll which decides if it will re-roll the that  
round.
o If that roll is true, then re-rolls and send the new result back.
• If user has above 60 credits, the function acts the same, but in this case  
the chance of re-rolling the round increases to 60%.
o If that roll is true, then the function re-rolls and send the new  
result back.
• There is a cash-out endpoint which moves credits from the game to  
user.


##• Client side: (UI):
o Include a super simple, minimalistic table with 3 blocks in 1 row.
o Include a button next to the table that starts the game.
o The components for each sign can be a starting letter (C for cherry, L for lemon, O for  orange, W for watermelon), but bonus points for using SVG assets (maybe get  
something from the internet).
o After submitting a roll-request to function, all blocks should enter a spinning state (can  be 'X' character spinning, but bonus points for getting spinner SVG from the internet). o After receiving response from the function, the first sign should spin for 1 second more  and then display the result, then display the second sign at 2 seconds, then the third  sign at 3 seconds.
o If the user wins the round, their credit is increased by the amount from the function call,  else it is deducted by 1.
o Include a button on the screen that says "CASH OUT", but when the user hovers it, there  is 50% chance that button moves in a random direction by 300px, and 40% chance that  it becomes unclickable.
• Write tests for your business logic
##Evaluation Criteria
- JS best practices
- Completeness: did you complete the features as briefed?
- Correctness: does the solution perform in sensible, thought-out ways?
- Maintainability: is the code written in a clean, maintainable way?
- Testing: was the system adequately tested?
  CodeSubmit
  Please organize, design, test and document your code as if it were going into production - then push  your changes to the master branch. You can have the repository on your account on Github, bitbucket  or Gitlab.  
  All the best and happy coding, 
