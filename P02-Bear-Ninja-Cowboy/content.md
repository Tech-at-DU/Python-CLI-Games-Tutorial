# Bear, Ninja, Cowboy

You might know the game as "Rock, Paper, Scissors"—but for the sake of this tutorial, we will be building a game of Bear, Ninja, Cowboy.

By the end of this chapter you will be able to:

1. Use the `input` keyword to get command line input from a user
1. Access values in an Array
1. Use the `random` method imported from the `randint` module native to Python
1. Use **Control Flow** if/else/elif statements
1. Use a `while` statement to make your game stay on
1. Use the keyword `break` to end the program

# Getting Started

Bear Ninja Cowboy or BNC will be made out of just one python file. You can tell if a file is python code if it ends in the `.py` document type.

If you don't already have one, navigate to the root of your computer, to the `~` directory, and make a new directory called `code`, then in that directory make a new directory called `cli-games`. We'll put all the games we make in this tutorial in this folder.

In that directory make a new file called `bnc.py`.

```bash
$ mkdir cli-games
$ cd cli-games
$ touch bnc.py
```

# Open the Directory in VSCode

```
$ code .
```

# Getting CLI Input

> What is code? An easy to understand definition is that **Code is very, very clear instructions for a computer**. As you start on the path to becoming a computer scientist and software engineer, start paying very close attention to the tiny details of code, because the computer will follow all code exactly as it is written.

Our first step to make a Bear, Ninja, Cowboy game is to get some input from players with the command line input.

Let's put in the absoulte least code we can to achieve our first goal of getting command line input.

```py
# cli-games/bnc.py

input = input("Greetings, what is your name? > ")
print("Greetings", input)
```

To run this file, we can use our terminal again if we are in the `cli-games` directory:

```bash
(cli-games)$ python3 bnc.py
```

You should see the input request, and if you type your name, you should see `"Greetings <<Your Name>>"` print out in the terminal.

## Updating For Our Purposes

Now we need to ask people not their name, but what role they'd like to play.

Update `bnc.py` to the following:

```py
# cli-games/bnc.py

player = input("Bear, Ninja, or Cowboy? > ")
print(player)
```

Now when we run the program, we should see the role the player has picked. If they write something else besides Bear, Ninja, or Cowboy, we'll deal with that later.

# Introducing Randomness

Bear Ninja Cowboy basically has four parts:

1. DONE - Command Line user input
1. The computer randomly picking a role
1. Checking the player's role and the computer's role
1. Displaying who won

We've already got some command line input coming in, so let's move on to randomly assigning the computer a role of either Bear, Ninja, or Cowboy.

In order to get a random role, we have to do three things, and to track those three we'll write three lines of commented out pseudocode:

```python
# Import the random library

# Make an array

# Generate a random number to pick a random element from the array
```

> **Comments and Pseudocode**: Notice that any code prefaced with a `#` pound sign is greyed out in your text editor. That is because everything to the right of a pound sign is not read by the computer. It is called a "Comment" or "Pseudocode" and is read only by humans.

## Filling in Pseudocode

Now that we have our pseudocode plan, we can start to write code for each line. We'll test it by printing the randomly selected role.

Update `bnc.py` to the following:

```python
# Import the random method from the randint module
from random import randint

# Define roles
roles = ["Bear", "Ninja", "Cowboy"]

# Generate a random role using an array
computer = roles[randint(0,2)]

print(computer)
```

Every time you run `$ python3 bnc.py` you should see one of the roles printed out.

# Check Who Wins

So now we have two of the four steps done. Let's do the next one. Check who won:

1. DONE - Command Line user input
1. DONE - The computer randomly picking a role
1. Checking the player's role and the computer's role
1. Displaying who won

To check both roles, we need to put the first two steps together:

```py
# cli-games/bnc.py

from random import randint

# Define roles
roles = ["Bear", "Ninja", "Cowboy"]

# Generate a random role using an array
computer = roles[randint(0,2)]

# Get player input
player = input("Bear, Ninja, or Cowboy? > ")

# Compare computer and player role

print(computer, player)
```

# DRAW!

We're going to break down the last step into a few sub-steps.

1. DONE - Command Line user input
1. DONE - The computer randomly picking a role
1. DONE - Checking the player's role and the computer's role
1. Displaying who won
      1. Display if there is a Draw
      1. Display if one of the three roles won
      1. Display if any of the three roles won

Now that we can see the computer's role and the player's role, we can setup some logic to compare the two.

First lets check if there is a draw:

```py
# cli-games/bnc.py
...
# Replace the print(computer, player) line with the following:
if computer == player:
  print("DRAW!")
else:
  print(computer, player)
```

The above code is called an `if/else statement`, it is part of a larger code pattern called **Control Flow** which is how software languages deal with and use Boolean Logic.

>**Boolean Logic** is a form of algebra which is centered around three simple words known as Boolean Operators: “Or,” “And,” and “Not”. At the heart of Boolean Logic is the idea that all values are either true or false. (lotame.com)

# Who Won?

So we have the DRAW case but we now need to check for win and loss cases. Let's do the case where the computer is a cowboy first. There are two options: the player can either be a bear (loses, cowboy shoots bear) or a ninja (wins, ninja defeats cowboy).

Update your `if` statement to include the following:

```py
# cli-games/bnc.py
...

if computer == player:
  print("DRAW!")
elif computer == "Cowboy":
  if player == "Bear":
    print("You lose!", computer, "shoots", player)
  else: # computer is cowboy, player is ninja
    print("You win!", player, "defeats", computer)
else:
  print(computer, player)
```

If you are missing some syntax, like a `:` or your indentation is off. You might get an error that looks like this:

```
  File "bnc-init.py", line 26
    elif computer == "Ninja"
                           ^
SyntaxError: invalid syntax
```

Treat errors like this as hints to how to fix your code so it works. In the case here, it means a `:` is missing at the end of the `elif` line.

If that's working, then we need to add other two other options.

```py
# cli-games/bnc.py
...

if computer == player:
  print("DRAW!")
elif computer == "Cowboy":
  if player == "Bear":
    print("You lose!", player, "is shot by", computer)
  else: # computer is cowboy, player is ninja
    print("You win!", player, "defeats", computer)
elif computer == "Bear":
  if player == "Cowboy":
    print("You win!", player, "shoots", computer)
  else: # computer is bear, player is ninja
    print("You lose!", player, "is eaten by", computer)
elif computer == "Ninja":
  if player == "Cowboy":
    print("You lose!", player, "is defeated by", computer)
  else: # computer is ninja, player is bear
    print("You win!", player, "eats", computer)
```

This is pretty good, but a bit weird because we probably expect the player to come first in every win/loss statement don't we...

Let's fix this using the passive voice.

```py
# cli-games/bnc.py

...
if computer == player:
  print("DRAW!")
elif computer == "Cowboy":
  if player == "Bear":
    print("You lose!", player, "is shot by", computer)
  else: # computer is cowboy, player is ninja
    print("You win!", player, "defeats", computer)
elif computer == "Bear":
  if player == "Cowboy":
    print("You win!", player, "shoots", computer)
  else: # computer is bear, player is ninja
    print("You lose!", player, "is eaten by", computer)
elif computer == "Ninja":
  if player == "Cowboy":
    print("You lose!", player, "is defeated by", computer)
  else: # computer is ninja, player is bear
    print("You win!", player, "eats", computer)
```

# Game Loop

So now we have a game, but do you notice how it ends right away every time? What if we wanted a smoother user experience and we wanted to play again and again. Or even offered a question "Do you want to play again?". In order to do this we need to use a `while` statement.

>`while` is a control flow word that tells a section of code to keep running so long as a condition is met.

After the `computer` gets assigned a role, replace all other code with the following:

```py
# cli-games/bnc.py

...

player = False

while player == False:
    # Get player input
    player = input("Bear, Ninja, or Cowboy? > ")

    # Compare computer and player role

    if computer == player:
      print("DRAW!")
    elif computer == "Cowboy":
      if player == "Bear":
        print("You lose!", computer, "shoots", player)
      else: # computer is cowboy, player is ninja
        print("You win!", player, "defeats", computer)
    elif computer == "Bear":
      if player == "Cowboy":
        print("You win!", player, "shoots", computer)
      else: # computer is bear, player is ninja
        print("You lose!", computer, "eats", player)
    elif computer == "Ninja":
      if player == "Cowboy":
        print("You lose!", computer, "defeats", player)
      else: # computer is ninja, player is bear
        print("You win!", player, "eats", computer)

    player = False
    computer = roles[randint(0,2)]
```

By setting `player` to `False` at the end keeps the `while` statement running forever. The only way to stop is to interrupt the process itself by tapping `control + c` on your keyboard.

# Play Again?

What if we didn't want the game to end, but prompted people to play again, how would we do that?

Let's make the user experience even cleaner by asking if people want to play again or not.

```py
# cli-games/bnc.py

...

    # after checking who won, put the following code

    play_again = input("Would you like to play again? (yes/no) > ")
    if play_again == 'yes':
      player = False
      computer = roles[randint(0,2)]
    else:
      break
```

We're using control flow again, this time to check if the input is `yes`. If it is yes, we want to keep `player` equal to `False` so the `while` statement keeps running and the game restarts. Otherwise, we want to end the program. That word `break` breaks off the program, ending it.

# More Features

What else could you add to this game?

Ever heard of [Rock, Paper, Scissors, Lizard, Spock](https://rpsls.net/#p4vrc)?

Anything else?

## Stretch Challenges

Try these ideas: 

- Currently inputting a not recognized name (like Anteater) wins two out of three times. You can solve this with a couple approaches. Test the input string and display a message if the name is not allowed for example: Ant is not Bear, Cowboy, or Ninja or Bear, Cowboy, and Ninja are the only allowed names. 
- Start the game with a get ready message! "Get ready to play Bear, Ninja, Cowboy!"
- Follow the start message with an option to get instructions. "Would you like instructions? (yes/no) >" If yes show some instructions, something like: "Bear, Ninja, Cowboy is an exciting game of strategy and skill! Pit your wit against the computer! Choose a player: Bear, Ninja, or Cowboy. The computer chooses a player. Bear eats Ninja, Ninja defeats Cowboy and cowboy shoots bear."
- Comment your code! Pay close attention to the formatting and code blocks. 
- Break your code into functions! Use functions to handle specific operations. Using functions is an important and coding best practice! 
- Keep score. Add 1 for each game you win subtract 1 for each game lost. Show the score after each game.
- Expand the game. Look up Rock, Paper, Scissors, Lizard, Spock. This is the same game but has five possible plays. Rock < Paper < Scissors < Lizard < Spock < Rock. 

# In Review: You Can ...

So in review here's what you did and what you can do now:

* You made your first Python 3 program, a Bear, Ninja, Cowboy game!
* You can access values in an array
* You can use the `input` keyword to get command line input from a user
* You can use the `random` method imported from the `randint` module native to Python
* You can use **Control Flow** if/else/elif statements
* You can use a `while` statement to make your game stay on
* You use the keyword `break` to end the program\

# Commit

Commit your changes to GitHub. Feel free to use a custom message of your own, as long as it accuratley describes what you did.

```bash
$ git add . && git commit -m "completed 'bear, ninja, cowboy' game'" && git push
```

# Next Steps

Almost done! Click [here](../P03-ASCII-Art/content.md) to move onto the next section about ASCII Art.
