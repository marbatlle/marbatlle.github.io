---
title: "Exercices from www.practicepython.org"
linktitle: 1. Basic Concepts Practice
toc: true
type: docs
date: "2019-05-05T00:00:00+01:00"
draft: false
menu:
  example:
    parent: Python
    weight: 1

# Prev/next pager order (if `docs_section_pager` enabled in `params.toml`)
weight: 1
---

## 1. Character input
### Nov 7, 2020

Create a program that asks the user to enter their name and their age. Print out a message addressed to them that tells them the year that they will turn 100 years old.

Extras:

1. Add on to the previous program by asking the user for another number and printing out that many copies of the previous message. (Hint: order of operations exists in Python)

2. Print out that many copies of the previous message on separate lines. (Hint: the string "\n is the same as pressing the ENTER button)


```python
# Name Input
name = input("Enter your name: ")

# Age Input
age = int(input("Enter your age: "))

# Age until 100
year_100 = (100 - age ) + 2020

# Output message
print(name + ", you will be 100 in " + str(year_100))

# Copies
copies = int(input("How many copies?: "))
print(copies * (name + ", you will be 100 in " + str(year_100) + "\n"))
```

    Enter your name: Mar
    Enter your age: 24
    Mar, you will be 100 in 2096
    How many copies?: 4
    Mar, you will be 100 in 2096
    Mar, you will be 100 in 2096
    Mar, you will be 100 in 2096
    Mar, you will be 100 in 2096
    


## 2. Odd or Even
### Nov 7, 2020

Ask the user for a number. Depending on whether the number is even or odd, print out an appropriate message to the user. Hint: how does an even / odd number react differently when divided by 2?

Extras:

1. If the number is a multiple of 4, print out a different message.
2. Ask the user for two numbers: one number to check (call it num) and one number to divide by (check). If check divides evenly into num, tell that to the user. If not, print a different appropriate message.


```python
# Number input
number = int(input("Enter a number: "))

# If even
if number % 2 == 0:
    print(str(number) + " is an even number")
else :
    print(str(number) + " is an odd number")

# Multiple of 4
if number % 4 == 0:
    print("And it's also a multiple of 4")
elif number % 2 == 0:
    print(str(number) + " is an even number")
else :
    print(str(number) + " is an odd number")

# Check
check = int(input("Enter a number: "))
num = int(input("Enter another number: "))
if check % num == 0:
    print(str(check) + " divides evenly into " + str(num))
else:
    print(str(check) + " doesn't divides evenly into " + str(num))
```

    Enter a number: 7
    7 is an odd number
    Enter a number: 10
    Enter another number: 2
    10 divides evenly into 2


## 3. List Less Than Ten
### Nov 7, 2020

Take a list and write a program that prints out all the elements of the list that are less than 5.

Extras:

1. Instead of printing the elements one by one, make a new list that has all the elements less than 5 from this list in it and print out this new list.
2. Write this in one line of Python.
3. Ask the user for a number and return a list that contains only elements from the original list a that are smaller than that number given by the user.


```python
list = [1, 4, 5, 6, 7, 3, 9, 8, 20]

# Print elements
for element in list:
    if element < 5:
        print(element)

# Create new list
new_list = []
for element in list:
    if element < 5:
        new_list.append(element)
print(new_list)


# Smaller than list
num = int(input("Enter a number: "))
list_user = []
for element in list:
    if element < num:
        list_user.append(element)
print(list_user)
    
```

    1
    4
    3
    [1, 4, 3]
    Enter a number: 19
    [1, 4, 5, 6, 7, 3, 9, 8]


## 4. Divisors
### Nov 7, 2020

Create a program that asks the user for a number and then prints out a list of all the divisors of that number. (If you don’t know what a divisor is, it is a number that divides evenly into another number. For example, 13 is a divisor of 26 because 26 / 13 has no remainder.)


```python
num = int(input("Please choose a number to divide: "))
divisors = []
listRange = range(1,num+1)

for elem in listRange:
    if num % elem == 0:
        divisors.append(elem)
print(divisors)
```


    ---------------------------------------------------------------------------

    KeyboardInterrupt                         Traceback (most recent call last)

    <ipython-input-76-e1a14ccfac8f> in <module>()
    ----> 1 num = int(input("Please choose a number to divide: "))
          2 divisors = []
          3 listRange = range(1,num+1)
          4 
          5 for elem in listRange:


    /home/marbatlle/miniconda3/envs/python/lib/python3.7/site-packages/ipykernel/kernelbase.py in raw_input(self, prompt)
        861             self._parent_ident,
        862             self._parent_header,
    --> 863             password=False,
        864         )
        865 


    /home/marbatlle/miniconda3/envs/python/lib/python3.7/site-packages/ipykernel/kernelbase.py in _input_request(self, prompt, ident, parent, password)
        902             except KeyboardInterrupt:
        903                 # re-raise KeyboardInterrupt, to truncate traceback
    --> 904                 raise KeyboardInterrupt("Interrupted by user") from None
        905             except Exception as e:
        906                 self.log.warning("Invalid Message:", exc_info=True)


    KeyboardInterrupt: Interrupted by user


## 5. List Overlap
### Nov 11, 2020
Take two lists, and write a program that returns a list that contains only the elements that are common between the lists (without duplicates). Make sure your program works on two lists of different sizes.

Extras:

1. Randomly generate two lists to test this
2. Write this in one line of Python (don’t worry if you can’t figure this out at this point - we’ll get to it soon)


```python
a = [1, 1, 2, 3, 5, 8, 13, 21, 34, 55, 89]
b = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 13]

#select repeated items
new_list = []

for num in a:
    if num in b:
        new_list.append(num)
print("Elements common between lists:", set(new_list))
```

    Elements common between lists: {1, 2, 3, 5, 8, 13}



```python
import random

#create 2 random lists
randa = []
randb = []

for a in range(0,40):
    a = random.randint(0,40)
    randa.append(a)
for b in range(0,40):
    b = random.randint(0,40)
    randb.append(b)

#delete duplicates in lists
rand_a = set(randa)
rand_b = set(randb)
    
#select repeated items
new_list = []
for num in rand_a:
    if num in rand_b:
        new_list.append(num)
print("Elements common between lists:", set(new_list))
```

    Elements common between lists: {34, 4, 5, 38, 7, 40, 20, 21, 22, 27, 28}


## 6. String Lists
### Nov 11, 2020

Ask the user for a string and print out whether this string is a palindrome or not.


```python
#ask user for string
wrd=input("Please enter a word")

#compare strings
if wrd == wrd[::-1]:
    print("This is a palindrom")
else:
    print("This is NOT a palindrom")
```

    Please enter a wordHoh
    This is NOT a palindrom


## 7. List Comprehensions
### Nov 12, 2020

Let’s say I give you a list saved in a variable: a = [1, 4, 9, 16, 25, 36, 49, 64, 81, 100]. Write one line of Python that takes this list a and makes a new list that has only the even elements of this list in it.


```python
a = [1, 4, 9, 16, 25, 36, 49, 64, 81, 100]
even = [num for num in a if num % 2 == 0]

print(even)
```

    [4, 16, 36, 64, 100]


## 8. Rock Paper Scissors
### Nov 12, 2020

Make a two-player Rock-Paper-Scissors game. (Hint: Ask for player plays (using input), compare them, print out a message of congratulations to the winner, and ask if the players want to start a new game)

Remember the rules:

* Rock beats scissors
* Scissors beats paper
* Paper beats rock


```python
user1 = input("Player 1, What's your name?: ")
user2 = input("Player 2, What's your name?: ")
play1 = input("%s, do you want to play rock, paper or scissors?: " % user1)
play2 = input("%s, do you want to play rock, paper or scissors?: " % user2)


def compare (user1_play, user2_play):
    if user1_play == user2_play:
        print("It's a tie!")
    elif user1_play == "rock":
        if user2_play == "scissors":
            print(user1 + " you won!")
        elif user2_play == "paper":
            print(user2 + " you won!")
    elif user1_play == "scissors":
        if user2_play == "rock":
            print(user2 + " you won!")
        elif user2_play == "paper":
            print(user1 + " you won!")
    elif user1_play == "paper":
        if user2_play == "scissors":
            print(user2 + " you won!")
        elif user2_play == "rock":
            print(user1 + " you won!")
    
compare(play1.lower(), play2.lower())
```

    Player 1, What's your name?: Mar
    Player 2, What's your name?: Mon
    Mar, do you want to play rock, paper or scissors?: Rock
    Mon, do you want to play rock, paper or scissors?: rock
    It's a tie!


## 9. Guessing Game One
### Nov 12, 2020

Generate a random number between 1 and 9 (including 1 and 9). Ask the user to guess the number, then tell them whether they guessed too low, too high, or exactly right.

Extras:

* Keep the game going until the user types “exit”
* Keep track of how many guesses the user has taken, and when the game ends, print this out.


```python
import random

num = random.randint(1,9)
guess = int(input("Guess the number between 1 and 9: "))

if num == guess:
    print("Congrats! You guessed the number!")
if num > guess:
    print("Your guess is too low...")
if num < guess:
    print("Your guess is too high..")
```

    Guess the number: 5
    Your guess is too high..



```python
import random

num = random.randint(1,9)
guess = 0
tries = 1

while guess != "exit" and guess != num:
    guess = input("Guess the number between 1 and 9: ")

    if guess == "exit":
        print("It's ok... you can't always win")
        break
    
    guess = int(guess)
    
    if num == guess:
        print("Congrats! You guessed the number!")
        if tries == 1:
            print("It only took you " + str(tries) + " try")
        else:
            print("It took you " + str(tries) + " tries")
            
    elif num > guess:
        tries = tries + 1
        print("Your guess is too low...")
        
    elif num < guess:
        tries = tries + 1
        print("Your guess is too high..")
        
```

    Guess the number between 1 and 9: 4
    Your guess is too high..
    Guess the number between 1 and 9: 3
    Your guess is too high..
    Guess the number between 1 and 9: 2
    Your guess is too high..
    Guess the number between 1 and 9: 1
    Congrats! You guessed the number!
    It took you 4 tries


## 10. List Overlap Comprehensions
### Nov 13, 2020

This week’s exercise is going to be revisiting an old exercise (see Exercise 5), except require the solution in a different way.

Take two lists,and write a program that returns a list that contains only the elements that are common between the lists (without duplicates). Make sure your program works on two lists of different sizes. Write this using at least one list comprehension. (Hint: Remember list comprehensions from Exercise 7).

Extra:

* Randomly generate two lists to test this


```python
a = [1, 1, 2, 3, 5, 8, 13, 21, 34, 55, 89]
b = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 13]
rep = [elem for elem in a if elem in b]


print(set(rep))
```

    {1, 2, 3, 5, 8, 13}



```python
import random

a = random.sample(range(100), 15)
b = random.sample(range(100), 17)

rep = [elem for elem in a if elem in b]

if len(rep) > 0:
    print(set(rep))
else:
    print("There are no matches")
```

    {82, 20, 95}


## 11. Check Primality Functions
### Nov 13, 2020

Ask the user for a number and determine whether the number is prime or not. (For those who have forgotten, a prime number is a number that has no divisors.). You can (and should!) use your answer to Exercise 4 to help you. Take this opportunity to practice using functions, described below.


```python
def is_prime(num = int(input("Give me a number: "))):

    divisors = [elem for elem in list(range(2,num)) if num % elem == 0]

    if len(divisors) == 0:
        
        print("It's a prime")
    else:
        print("NOT a prime, it can be divided by:", divisors)

is_prime(num)
```

    Give me a number: 749
    It's a prime


## 12. List Ends
### Nov 13, 2020
Write a program that takes a list of numbers (for example, a = [5, 10, 15, 20, 25]) and makes a new list of only the first and last elements of the given list. For practice, write this code inside a function.


```python
import random
list = random.sample(range(100),int(input("Elements in the list:")))
def first_last(list):
    print("The first number is",list[0],"and the last one",list[-1])

first_last(nums)
```

    Elements in the list:5
    The first number is 39 and the last one 76


## 13. Fibonacci
### Nov 13, 2020

Write a program that asks the user how many Fibonnaci numbers to generate and then generates them. Take this opportunity to think about how you can use functions. Make sure to ask the user to enter the number of numbers in the sequence to generate.(Hint: The Fibonnaci seqence is a sequence of numbers where the next number in the sequence is the sum of the previous two numbers in the sequence. The sequence looks like this: 1, 1, 2, 3, 5, 8, 13, …)


```python
def gen_fib(loops = int(input("numbers "))):
    if loops == 0:
        print("If you don't want any number...")
        fib = []
    elif loops == 1:
        fib = [1]
    elif  loops == 2:
        fib = [1,1]
    else:
        fib = [1,1]
        loops -= 2
        while loops > 0: 
            fib.append((fib[-1]+fib[-2]))
            loops -= 1
    return fib
    
gen_fib()
```

## 14. List Remove Duplicates
### Nov 13, 2020

Write a program (function!) that takes a list and returns a new list that contains all the elements of the first list minus all the duplicates.

Extras:

* Write two different functions to do this - one using a loop and constructing a list, and another using sets.
* Go back and do Exercise 5 using sets, and write the solution for that in a different function.


```python
# Using loop
def no_duplicates (lst):
    new_list = []
    for i in lst:
        if i not in new_list:
            new_list.append(i)
    return new_list

a = [1,2,4,7,5,6,7]
no_duplicates(a)
```




    [1, 2, 4, 7, 5, 6]




```python
# Using set
def no_duplicates(lst):
    new_list = set(lst)
    return list(set(lst))

a = [1,2,4,7,5,6,7]
no_duplicates(a)
```




    [1, 2, 4, 5, 6, 7]



## 15. Reverse Word Order
### Nov 13, 2020

Write a program (using functions!) that asks the user for a long string containing multiple words. Print back to the user the same string, except with the words in backwards order. 


```python
str1 = input("Tell me something")

list1 = a.split(" ")
list1.reverse()
str2 = ' '.join(list1)

print(str2)
```


    ---------------------------------------------------------------------------

    KeyboardInterrupt                         Traceback (most recent call last)

    <ipython-input-101-fc8d927c741a> in <module>()
    ----> 1 str1 = input("Tell me something")
          2 
          3 list1 = a.split(" ")
          4 list1.reverse()
          5 str2 = ' '.join(list1)


    /home/marbatlle/miniconda3/envs/python/lib/python3.7/site-packages/ipykernel/kernelbase.py in raw_input(self, prompt)
        861             self._parent_ident,
        862             self._parent_header,
    --> 863             password=False,
        864         )
        865 


    /home/marbatlle/miniconda3/envs/python/lib/python3.7/site-packages/ipykernel/kernelbase.py in _input_request(self, prompt, ident, parent, password)
        902             except KeyboardInterrupt:
        903                 # re-raise KeyboardInterrupt, to truncate traceback
    --> 904                 raise KeyboardInterrupt("Interrupted by user") from None
        905             except Exception as e:
        906                 self.log.warning("Invalid Message:", exc_info=True)


    KeyboardInterrupt: Interrupted by user



```python
def reverseWord(w):
    return ' '.join(w.split()[::-1])

w = input("Tell me something: ")
reverseWord(w)
```

    Tell me something: me llamo mar





    'mar llamo me'



## 16. Password Generator
### Nov 15, 2020

Write a password generator in Python. Be creative with how you generate passwords - strong passwords have a mix of lowercase letters, uppercase letters, numbers, and symbols. The passwords should be random, generating a new password every time the user asks for a new password. Include your run-time code in a main method.

Extra:

* Ask the user how strong they want their password to be. For weak passwords, pick a word or two from a list.


```python
import random

def generate_password(pass_len):

    s = "abcdefghijklmnopqrstuvwxyz01234567890ABCDEFGHIJKLMNOPQRSTUVWXYZ!@#$%^&*()?"

    p =  "".join(random.sample(s,pass_len))

    return p

generate_password(int(input("Password lenght: ")))
```

    Password lenght: 8





    '#q*ZMyt7'




```python
import random

pass_str = ["Weak", "Normal", "Strong"]
user_str = input("How strong do you want your password?\n\n- " + pass_str[0] + "\n- " + pass_str[1] + "\n- " + pass_str[2] + "\n\n")

if user_str == pass_str[0]:
    s = ["hello", "password", "baby", "1996", "python", "barcelona"]
    print("".join(random.sample(s, 2)))

elif user_str == pass_str[1]: 
    s = "abcdefghijklmnopqrstuvwxyz01234567890"
    print("".join(random.sample(s,8)))
else:
    s = "abcdefghijklmnopqrstuvwxyz01234567890ABCDEFGHIJKLMNOPQRSTUVWXYZ!@#$%^&*()?"
    print("".join(random.sample(s,8)))
    
    

```

    How strong do you want your password?
    
    - Weak
    - Normal
    - Strong
    
    Strong
    BM&TrZqX


## Decode a Web Page
### Nov 15, 2020

Use the BeautifulSoup and requests Python packages to print out a list of all the article titles on the New York Times homepage.


```python
# import the requests Python library for programmatically making HTTP requests
# after installing it according to these instructions: 
# http://docs.python-requests.org/en/latest/user/install/#install
import requests

# import the BeautifulSoup Python library according to these instructions: 
# http://www.crummy.com/software/BeautifulSoup/bs4/doc/#installing-beautiful-soup
# use this syntax as described on the documentation page: 
# http://www.crummy.com/software/BeautifulSoup/bs4/doc/#making-the-soup
from bs4 import BeautifulSoup

# the URL of the NY Times website we want to parse
base_url = 'http://www.nytimes.com'

# the syntax (according to the documentation) for how to 
# "load" a webpage through Python
r = requests.get(base_url)

# how to decode the text of the HTML of the NY Times homepage
# website. r comes from the requests request above
soup = BeautifulSoup(r.text)

# find and loop through all elements on the page with the 
# class name "story-heading"
for story_heading in soup.find_all(class_="story-heading"): 
    # for the story headings that are links, print out the text
    # and format it nicely
    # for the others, take the contents out and format it nicely
    if story_heading.a: 
        print(story_heading.a.text.replace("\n", " ").strip())
    else: 
        print(story_heading.contents[0].strip())
```


```python
import requests
from bs4 import BeautifulSoup

r = requests.get('https://news.ycombinator.com/')

r_html = r.text

soup = BeautifulSoup(r_html, 'html.parser')

title = soup.find_all("a", "storylink")

articleNames = []

for x in title:
    titlestring = x.string
    articleNames.append(titlestring)

for x in articleNames:
    print(x)
```

    Create Vintage Videos Using FFmpeg in 4 Simple Steps
    UK to ban sale of new petrol and diesel cars from 2030: FT
    Electrified wingsuit from BMW reaches 186MPH on first flight
    Sourcehut's Second Year in Alpha
    Show HN: LibreASR – An On-Premises, Streaming Speech Recognition System
    Bitmovin (YC S15) Is Hiring Sales, Support and Engineering in Denver
    Why to Start a Startup in a Bad Economy (2008)
    The Messaging Layer Security (MLS) Protocol
    BetterExplained: Clear, intuitive lessons about mathematics
    Moving my serverless project to Ruby on Rails
    A Remembrance of Forrest Fenn
    Pydis – Redis clone in 250 lines of Python, for performance comparison
    Soumitra Chatterjee: India acting legend dies, aged 85
    The first open-source ventilator tested on human patients
    PinePhone – KDE Community edition
    Ori Pocket Office
    Better disposable coffee cups can be made with waste from sugar cane
    Rudy the Red Dot
    VLC and Qt – A History [video]
    On Taking Criticism
    Small Copy, Big Impact
    Bypassing Firewalls in macOS Big Sur
    Why I teach vim
    Herman Mankiewicz, Pauline Kael, and the Battle over “Citizen Kane”
    OpenSUSE MicroOS
    Open Source does not mean “Includes Free Support”
    Ask HN: Am I too late for the “Data Science” wave?
    Neil Postman on Cyberspace (1995) [video]
    Conservatives flock to Parler, claiming censorship on Facebook and Twitter
    An Interactive Introduction to Fourier Transforms


## Cows and Bulls
### Nov 15, 2020

Create a program that will play the “cows and bulls” game with the user. The game works like this:

Randomly generate a 4-digit number. Ask the user to guess a 4-digit number. For every digit that the user guessed correctly in the correct place, they have a “cow”. For every digit the user guessed correctly in the wrong place is a “bull.” Every time the user makes a guess, tell them how many “cows” and “bulls” they have. Once the user guesses the correct number, the game is over. Keep track of the number of guesses the user makes throughout teh game and tell the user at the end.


Say the number generated by the computer is 1038. An example interaction could look like this:

  Welcome to the Cows and Bulls Game! 
  * Enter a number: 
  * 1234
  * 2 cows, 0 bulls
  * 1256
  * 1 cow, 1 bull
  * ...
  
Until the user guesses the number.


```python
import random

print("Welcome to the Cows and Bulls Game?")

random = random.sample(range(9),4)

while True:
    guess = int(input("Enter a 4 digit number: "))
    guess = [int(x) for x in str(guess)]
    cows = 0
    bulls = 0
    count = 0
    
    if guess == random:
        print("You won the game!")
        break
    else:
        for i in range(0,4):
            if guess[i] == random[i]:
                cows += 1
            elif random[i] in guess:
                bulls += 1
        
    print("You have " + str(cows)+ " cows, and " + str(bulls) + " bulls")

```

    Welcome to the Cows and Bulls Game?
    Enter a 4 digit number: 1234
    You have 0 cows, and 2 bulls
    Enter a 4 digit number: 1256
    You have 1 cows, and 1 bulls
    Enter a 4 digit number: 1243
    You have 0 cows, and 2 bulls
    Enter a 4 digit number: 8843
    You have 0 cows, and 1 bulls
    Enter a 4 digit number: 8838
    You have 0 cows, and 1 bulls
    Enter a 4 digit number: 8858
    You have 0 cows, and 0 bulls
    Enter a 4 digit number: 8884
    You have 0 cows, and 0 bulls
    Enter a 4 digit number: 1888
    You have 0 cows, and 0 bulls
    Enter a 4 digit number: 8288
    You have 0 cows, and 1 bulls
    Enter a 4 digit number: 2888
    You have 0 cows, and 1 bulls
    Enter a 4 digit number: 8828
    You have 1 cows, and 0 bulls
    Enter a 4 digit number: 9929
    You have 1 cows, and 0 bulls
    Enter a 4 digit number: 1234
    You have 0 cows, and 2 bulls
    Enter a 4 digit number: 8881
    You have 0 cows, and 0 bulls
    Enter a 4 digit number: 8883
    You have 0 cows, and 1 bulls
    Enter a 4 digit number: 3888
    You have 0 cows, and 1 bulls
    Enter a 4 digit number: 8388
    You have 1 cows, and 0 bulls
    Enter a 4 digit number: 8328
    You have 2 cows, and 0 bulls
    Enter a 4 digit number: 4888
    You have 0 cows, and 0 bulls
    Enter a 4 digit number: 5888
    You have 0 cows, and 0 bulls
    Enter a 4 digit number: 6888
    You have 0 cows, and 1 bulls
    Enter a 4 digit number: 8326
    You have 3 cows, and 0 bulls
    Enter a 4 digit number: 7326
    You won the game! It took you 0 guesses


## Element Search
### Nov 18, 2020

Write a function that takes an ordered list of numbers (a list where the elements are in order from smallest to largest) and another number. The function decides whether or not the given number is inside the list and returns (then prints) an appropriate boolean.

Extras:

* Use binary search.


```python
a = [1,2,3,4,5,6,7,8,9]
b = 7

def find_number(num, lst):
    for i in lst:
        truth_value = num == i
        if (truth_value):
            return True
    return False

find_number(b,a)
```




    False



## Draw a Game Board
### Nov 18, 2020

Ask the user what size game board they want to draw, and draw it for them to the screen using Python’s print statement.


```python
# ask for desired board size
board_size = int(input("What size of game board? "))
count = board_size
while True:
    if count > 0:
        print(" ---" * board_size)
        print("|   " * (board_size + 1))
        count -= 1
    if count == 0:
        print(" ---" * board_size)
        break
        
```

    What size of game board? 4
     --- --- --- ---
    |   |   |   |   |   
     --- --- --- ---
    |   |   |   |   |   
     --- --- --- ---
    |   |   |   |   |   
     --- --- --- ---
    |   |   |   |   |   
     --- --- --- ---



```python
def print_horiz_line():
    print(" ---" * board_size)
def print_vert_line():
    print("|   " * (board_size + 1))
    
board_size = int(input("What size of game board? "))

for i in range(board_size):
    print_horiz_line()
    print_vert_line()
print_horiz_line()   
```

    What size of game board? 3
     --- --- ---
    |   |   |   |   
     --- --- ---
    |   |   |   |   
     --- --- ---
    |   |   |   |   
     --- --- ---


## Guessing Game Two
### Nov 18, 2020

In a previous exercise, we’ve written a program that “knows” a number and asks a user to guess it.

This time, we’re going to do exactly the opposite. You, the user, will have in your head a number between 0 and 100. The program will guess a number, and you, the user, will say whether it is too high, too low, or your number.

At the end of this exchange, your program should print out how many guesses it took to get your number.

As the writer of this program, you will have to choose how your program will strategically guess. A naive strategy can be to simply start the guessing at 1, and keep going (2, 3, 4, etc.) until you hit the number. But that’s not an optimal guessing strategy. An alternate strategy might be to guess 50 (right in the middle of the range), and then increase / decrease by 1 as needed. After you’ve written the program, try to find the optimal strategy! (We’ll talk about what is the optimal one next week with the solution.)


```python
my_list = range(0,100)
while True:
    center_index = int(len(my_list)/2)
    guess = my_list[center_index]
    user_input = input("Is the number " + str(guess) + " ?")
    if user_input == "too high":
        my_list = my_list[:center_index]
    elif user_input == "too low":
        my_list = my_list[center_index:]
    elif user_input == "yes":
        print("The machine won! ;)")
        break
    else:
        print("Response has to be: too high, too low or yes")
```

    Is the number 50 ?yes
    The machine won! ;)



```python

```


```python

```


```python

```


```python

```


```python

```
