---
title: "Flash Card Tester"
slug: flash-cards
---

Ever need to memorize something? Flash cards can really do the trick! So we're going to build a command line flash card tester application. Let's get started.

By the end of this chapter you will be able to:

1. Read a file with python3
1. Parse data from a **JSON** format into a python **dictionary**
1. Iterate over an array
1. Take user input from the command line

# Getting Started

Flash Cards will be made out of just one python file. You can tell if a file is python code if it ends in the `.py` document type.

If you don't already have one, navigate to the root of your computer, to the `~` directory, and make a new directory called `code`, then in that directory make a new directory called `cli-games`. We'll put all the games we make in this tutorial in this folder. In that directory make a new directory called `flash-cards` and in that directory make two files, one called `flashcards.py` and one called `me-capitals.json` (where we will put our flash card data of "Middle Eastern Capitals").

```bash
$ cd ~
$ mkdir code
$ cd code
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

# Open the Directory in Atom

Using the [atom text editor](https://atom.io/) open the `flash-cards` directory using the `atom` command within the `flash-cards` directory:

```
(flash-cards)$ atom .
```

Now let's get started with the code.

We have basically five steps:

1. Setup the data
1. Write code that reads the data file and parses it into a python dictionary
1. Write code that iterates over the data
1. Get the users's input for each question
1. Check the users input against the answer and display "Correct!" or "Incorrect!"


# Setting Up Data

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

>[info]
> JSON is a very popular way to store and transmit data in the internet. It is a great format for data because it is easy for computers and humans to read it and write it.
> JSON's basic structure is comma-delimited **Key-Value Pairs** surrounded by curly-bracies `{}`. Notice that keys are strings, and values can be any form of data, including arrays `[]`, and objects `{}`. By having arrays and objects as values gives JSON a nested tree structure. As you use JSON more you will become very familiar with its structure.

This bit of JSON has one root key called `cards`, and the value associated with `cards` is an array of cards. Each element in the array `[]` is an object `{}` with two keys `q` for "question" and `a` for "answer".

# Read a File

A python script `.py` can read files around it using file system commands native to python.

Let's use these commands to read the `me-capitals.json` file and parse the JSON into a data format python can manipulate: a **Dictionary**. (Python can't work with JSON itself, it has to change it into an equivalent structure that it understands).

Now we need to read this file and print its contents.

```py
# import the json module from python3
import json

# open the file and parse the JSON
with open('me-capitals.json', 'r') as f:
    data = json.load(f)
    print(data)
```

First we import the `json` module and then we use the use the `open` built-in function, and pass it two arguments:

  1. the name of the file: `me-capitals.json`
  1. An option—in this case `'r'`, which just means "read"

The `as f:` part means that the contents of the file is passed into the `open` function as the variable f.

So finally we use the `json` module we imported above to `.load(f)` that is to load the contents of the file and parse it from json into a python dictionary called `data`.

Test the code by running:

```
$ python3 flashcards.py
```

You should see the contents of the file. The only difference between JSON and a python dictionary is the keys have `''` single quotes whereas the JSON has `""` double-quotes. Now that you are an engineer, you should be aware and focus on tiny differences like that b/c they matter to the computer.

# For Loop Iterator

We've completed the first two steps, so next we have to iterate over the `cards` array:

1. DONE - Setup the data
1. DONE - Write code that reads the data file and parses it into a python dictionary
1. Write code that iterates over the data
1. Get the users's input for each question
1. Check the users input against the answer and display "Correct!" or "Incorrect!"

>[info]
>**Iterating** over something in code is like a teacher calling roll. The teacher calls out a name in their list of students. Each student responds present if they are present, and there is no response if they are absent. In code, you could say the teacher **iterates** through the array of students and calls a function that returns “present” if the student is present, otherwise it returns "<<silence>>".

We will use what is called a For Loop iterator to iterate over all the cards. The For Loop has this structure:

```py
for <<ITEM>> in <<LIST or ARRAY>>
```

So in our case for our cards:

```py
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

Run the program.

## A Few More Questions

We're using learning the capitals of countries in the middle east for our cards. Let's add a few more capitals to our `me-capitals.json` file:

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

Ok now we need to get the user to actually try to answer each question. To access the question in each object, we'll need to use the same way we accessed `cards` inside of data: `i["q"]`. And we'll use the `input` built-in function to prompt the user to enter an input.

```py
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

```py
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

# Adding the Correct Answer When Incorrect

Now let's polish up the user experience by display the correct answer when someone get's the answer wrong.

```py
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

Now the comparison is only between all lowercase text no matter what.

# Brainstorm New Features

What else could you add to this program? Here are some ideas:

1. As them if they want to play again at the end.
1. Randomize the order of questions.
1. Keep playing until the player gets all the questions right at least once.
1. Keep playing until the player answers correctly 10 in a row.
1. Create various `data` files that are different sets of questions and let people pick which one they want to do.
1. Let people enter their own cards and save those as libraries of questions and answers.

As a stretch challenge now or later, come back and try to implement one of these. But let's do one of them right now.

# Keeping Track of Score

Let's use a variable called `score` to keep track of score with each answer.

```py
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
        ++score
        # interpolate score and total into the response
        print(f"Correct! Current score: {score}/{total}")
    else:
        print("Incorrect! The correct answer was", i["a"])
        print(f"Current score: {score}/{total}")
```

Examine the code above and look at the comments. You can see that we have made 4 changes:

1. We initialized `total` as the length of the cards array using the `len(array)` built-in function.
1. We initialized `score` as 0 because everyone starts with 0 correct answers.
1. Next when they get a write answer we **increment** `score` by 1 using the `++` increment operator of python.
1. Finally we use a new feature of Python 3.6 called **f-strings** to interpolate `{score}` and `{total}` to our response in the correct and incorrect messages.

Check and see if yours works and troubleshoot any errors.

## Stretch: f-strings

Can you use **f-strings** to change how we do string interpolations throughout this program?

# In Review: You Can ...

So in review here's what you did and what you can do now:

1. You can read a file with python3
1. You can parse data from a **JSON** format into a python **dictionary**
1. You can access elements in a python dictonary
1. You can iterate over an array
1. You can take user input from the command line