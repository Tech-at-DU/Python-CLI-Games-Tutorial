# Flash Card Tester

Ever need to memorize something? Flash cards can really do the trick! So we're going to build a command line flash card tester application. Let's get started.

Imagine you want to learn the capitals of countries in the Middle East. Let's make some flashcards.

By the end of this chapter you will be able to:

1. Read a file with python3
1. Parse data from a **JSON** format into a python **dictionary**
1. Iterate over an array
1. Take user input from the command line

# Getting Started

Flash Cards will be made out of just one python file. You can tell if a file is python code if it ends in the `.py` document type.

If you don't already have one, navigate to the root of your computer, to the `~` directory, and make a new directory called `code`, then in that directory make a new directory called `cli-games`. We'll put all the games we make in this tutorial in this folder. In that directory make a new directory called `flash-cards` and in that directory make two files, one called `flashcards.py` and one called `me-capitals.json` (where we will put our flash card data of "Middle Eastern Capitals").

Make your initial project folder and two main files:

```bash
$ cd to/your/code/directory
$ mkdir cli-games
$ cd cli-games
$ mkdir flash-cards
$ cd flash-cards
$ touch flashcards.py
$ touch me-capitals.json
```

Now your folder should look like this:

```
| cli-games
  | flash-cards
    |- flashcards.py
    |- me-capitals.json
  ...
```

>It is important to keep your coding projects organized on your computer. Having a centralized folder called `code` or `dev` where you put all projects is a great pattern to follow.

# Setting up GitHub Repo

It would be a good idea to setup our GitHub repository now before we go any futher.

If this is your first time using GitHub CLI, you are going to need to log into GitHub. Run `gh auth login` in your terminal to login with your GitHub.com account. You can authenticate either through HTTPS or SSH. If you are not familiar with SSH, choose the
HTTPS option and follow the provided steps to login.

Additionally, if you are currently in the `flash-cards` directory, `cd` out of it to the main `cli-games` folder with the `cd -` command in order to add the entire project to the repo.

Now it's time to setup our repo. Run the following commands in terminal and then follow the interactive prompts:

```bash
$ git init -b main
$ gh repo create python-cli-games-tutorial
```

# Open the Directory in VSCode

Let's try using the command line command `code .` to open the directory we are currently in. Make sure you have navigated to the `flash-cards` directory, then type the following:

```
(flash-cards)$ code .
```

**Clarification** - The period (`.`) in `code .` means "this directory". You can also open a project using a path, e.g. from the root `~` type the command `$ code code/cli-games`

# Make a Plan

Software engineers always start any work by writing up a plan for how they will work on a project. This tutorial will provide you with this plan to start off with:

We have basically five steps:

1. Setup the cards data that we want to quiz ourselves with
1. Write code that reads the cards data and parses it into a python dictionary
1. Write code that iterates over the cards
1. Get the users's input for each question
1. Check the users input against the answer
1. Display "Correct!" or "Incorrect!"

# Setting up Virtual Environment

Take a moment to setup your Virtual Environment.

If you haven't setup a virtual environment before, make sure install it with the command `python3 -m pip install --user virtualenv`

Otherwise, make sure you are in the main directory of the project and run the following to create your virtualenv:

```bash
$ python3 -m venv env
$ source env/bin/activate
```

# Setting Up Card Data

Let's imagine we have a list of Middle Eastern countries and their capitals. Let's write those into a format called JSON.

Go into your `me-capitals.json` file and let's add a little bit of JSON.

```json
{
  "cards": [
    {
      "q": "What is the capital of Syria?",
      "a": "Damascus"
    }
  ]
}
```

This bit of JSON has one root key called `cards`, and the value associated with `cards` is an array of cards. Each element in the array `[]` is an object `{}` with two keys `q` for "question" and `a` for "answer".

> JSON is a very popular way to store and transmit data in the internet. It is a great format for data because it is easy for computers and humans to read it and write it.
> JSON's basic structure is comma-delimited **Key-Value Pairs** surrounded by curly-bracies `{}`. Notice that keys are strings, and values can be any form of data, including arrays `[]`, and objects `{}`. By having arrays and objects as values gives JSON a nested tree structure. As you use JSON more you will become very familiar with its structure.

Check your JSON with the JSON Validator/formatter: https://jsonformatter.curiousconcept.com

# Read a File

A python script `.py` can read files around it using file system commands native to python.

Let's use these commands to read the `me-capitals.json` file and parse the JSON into a data format python can manipulate: a **Dictionary**. (Python can't work with JSON itself, it has to change it into an equivalent structure that it understands).

```py
# flashcards.py

# import the json module from python3
import json

# open the file and parse the JSON
with open('me-capitals.json', 'r') as f:
    data = json.load(f)
    print(data)
```

First we import the `json` module and then we use the use the `open` built-in function, and pass it two arguments:

  1. The name of the file: `me-capitals.json`
  1. An option—in this case `'r'`, which just means "read"

The `as f:` part means that the contents of the file is passed into the `open` function as the variable f.

So finally we use the `json` module we imported above to `.load(f)` that is to load the contents of the file and parse it from json into a python dictionary called `data`.

Always test your code after each step by running it and checking that the step you just completed is working. Run your project with this command:

```
$ python3 flashcards.py
```

When you run this, you should see the contents of the file:

```
{'cards': [{'q': 'What is the capital of Syria?', 'a': 'Damascus'}]}
```

The only difference between JSON and a python dictionary is the keys have `''` single quotes whereas the JSON has `""` double-quotes. Now that you are an engineer, you should be aware and focus on tiny differences like that because they matter to the computer.

# For Loop Iterator

We've completed the first two steps, so next we have to iterate over the `cards` array:

1. DONE - Setup the data
1. DONE - Write code that reads the data file and parses it into a python dictionary
1. Write code that iterates over the data
1. Get the users's input for each question
1. Check the users input against the answer and display "Correct!" or "Incorrect!"

>**Iterating** over something in code is like a teacher calling roll. The teacher calls out a name in their list of students. Each student responds present if they are present, and there is no response if they are absent. In code, you could say the teacher **iterates** through the array of students and calls a function that returns “present” if the student is present, otherwise it returns "<<silence>>".

We will use what is called a For Loop iterator to iterate over all the cards. The For Loop has this structure:

```py
for <<ITEM>> in <<LIST or ARRAY>>
```

Let's add a for loop to our flashcards:

```py
# flashcards.py

# import the json module from python3
import json

# open the file and parse the JSON
with open('me-capitals.json', 'r') as f:
    data = json.load(f)

for i in data["cards"]:
    print(i)
```

`data["cards"]` is the way to access a value in a key-value pair inside a python dictionary. Since the structure looks like this:

```py
{'cards': [{'q': 'What is the capital of Syria', 'a': 'Damascus'}]}
```

We need to access the `cards` key, to get back its array value `[{'q': 'What is the capital of Syria', 'a': 'Damascus'}]`.

Run the program again using `python3 flashcards.py` and make sure you get output as described above

# A Few More Questions

We're using learning the capitals of countries in the middle east for our cards.

Let's add a few more capitals to our `me-capitals.json` file:

```json
{
  "cards": [
    {
      "q": "What is the capital of Syria?",
      "a": "Damascus"
    },
    {
      "q": "What is the capital of Lebanon?",
      "a": "Beirut"
    },
    {
      "q": "What is the capital of Israel?",
      "a": "Jerusalem"
    },
    {
      "q": "What is the capital of Jordan?",
      "a": "Amman"
    },
    {
      "q": "What is the capital of Iraq?",
      "a": "Baghdad"
    }
  ]
}
```

Now rerun the program and see if your iterator prints out each question

# Getting CLI Input

Ok now we need to get the user to actually try to answer each question. To access the question in each object, we'll do so using the same way we accessed `cards` inside of data: `i["q"]`. And we'll use the `input` built-in function to prompt the user to enter an input.

Update `flashcards.py` to the following:

```py
# flashcards.py

# import the json module from python3
import json

# open the file and parse the JSON
with open('me-capitals.json', 'r') as f:
    data = json.load(f)

for i in data["cards"]:
    guess = input(i["q"] + " > ")
    print(guess)
```

Run this program and see that you can see your guess printed out.

# Check For Correct Answer

So now we've done four of our five steps we set out to do, so all we have now is to check if the answer is right:

1. DONE - Setup the data
1. DONE - Write code that reads the data file and parses it into a python dictionary
1. DONE - Write code that iterates over the data
1. DONE - Get the users's input for each question
1. Check the users input against the answer and display "Correct!" or "Incorrect!"

We'll check correct and incorrect using the equality operator: `==`.

Update your for loop in `flashcards.py` to the following:

```py
# flashcards.py

import json

with open('me-capitals.json', 'r') as f:
    data = json.load(f)

for i in data["cards"]:
    guess = input(i["q"] + " > ")

    if guess == i["a"]:
        print("Correct!")
    else:
        print("Incorrect!")
```

>A note on **Clear Variable Naming**. Variables can be named almost anything, so it is important to pick names that are logical and semantic. We named the user's input "guess" because in terms of this program, that is what it is, the user's input is a guess at what the flashcard's answer is. Always consider carefully what to name a variable and pick a logical and clear name.

# Adding the Correct Answer When Incorrect

Now let's polish up the user experience by display the correct answer when someone get's the answer wrong.

```py
# flashcards.py

import json

with open('me-capitals.json', 'r') as f:
    data = json.load(f)

for i in data["cards"]:
    guess = input(i["q"] + " > ")

    if guess == i["a"]:
        print("Correct!")
    else:
        print("Incorrect! The correct answer was", i["a"])
```

Run the program and see how this looks. Pretty good?

# Case Sensitivity

Notice right now that if you enter "jerusalem" instead of "Jerusalem" you get the answer wrong. We could remove this, but capitals are capitalized aren't they.

But what if we want to make other cards for biology or French words? Capitalizing the answer exactly will be annoying.

To fix this we can use the `string.lower()` string function to lowercase the whole word before we compare them.

```py
...

if guess.lower() == i["a"].lower():

...
```

Now the comparison is only between all lowercase text no matter what. You can try this out by changing the code in `flashcards.py` if you want to see it in action.

# Brainstorm New Features

What else could you add to this program? Here are some ideas:

1. Ask them if they want to play again at the end.
1. Randomize the order of questions.
1. Keep playing until the player gets all the questions right at least once.
1. Keep playing until the player answers correctly 10 in a row.
1. Create various `data` files that are different sets of questions and let people pick which one they want to do.
1. Let people enter their own cards and save those as libraries of questions and answers.

As a **stretch challenge** now or later, come back and try to implement one of these. But let's do one of them right now.

# Keeping Track of Score

Let's use a variable called `score` to keep track of score with each answer.

Update `flashcards.py` to the following:

```py
# flashcards.py
import json

with open('me-capitals.json', 'r') as f:
    data = json.load(f)

# initialize total as the length of the cards array
total = len(data["cards"])
# initialize score as 0
score = 0

for i in data["cards"]:
    guess = input(i["q"] + " > ")

    if guess == i["a"]:
        # increment score up one
        score += 1
        # interpolate score and total into the response
        print(f"Correct! Current score: {score}/{total}")
    else:
        print("Incorrect! The correct answer was", i["a"])
        print(f"Current score: {score}/{total}")
```

Examine the code above and look at the comments. You can see that we have made 4 changes:

1. We initialized `total` as the length of the cards array using the `len(array)` built-in function.
1. We initialized `score` as 0 because everyone starts with 0 correct answers.
1. Next when they get a right answer we **increment** `score` by 1 using `+= 1`
1. Finally we use a new feature of Python 3.6 called **f-strings** to interpolate `{score}` and `{total}` to our response in the correct and incorrect messages.

Check and see if yours works and troubleshoot any errors.
 
## Stretch Challenges: 
  
- f-strings - Can you use **f-strings** to change how we do string interpolations throughout this program?
- End game message - print a message when the game ends, something like: "Thanks for playing! You scored: 4 out five correct!"
  - To find the number of questions `len()` to count the cards array.
  - Modify the message based on the score: 
    - Less than half correct: "You need practice..."
    - More than half correct: "Good work..."
    - All correct: "Amazing..."
- Use functions to organize your code. 
  - Use a function to read the data file. 
    - This function might take the file path as a parameter
    - And return the data that was loaded
  - Use a function to display the next question
    - This function might take the question and the answer as a parameter
    - And return True or False if the question was answered correctly
  - Write a function to display game messages
    - You might have a function to display a starting message
    - You might have a quwstion to display an end game message

# In Review: You Can ...

So in review here's what you did and what you can do now:

1. You can read a file with python3
1. You can parse data from a **JSON** format into a python **dictionary**
1. You can access elements in a python dictionary
1. You can iterate over an array
1. You can take user input from the command line

# Commit

Commit your changes to GitHub. Feel free to use a custom message of your own, as long as it accuratley describes what you did.

```bash
$ git add . && git commit -m "completed flash card tester" && git push
```

# Next Steps

Click [here](../P02-Bear-Ninja-Cowboy/content.md) to move onto the next section about making a game similar to "Rock, Paper, Scissors".
