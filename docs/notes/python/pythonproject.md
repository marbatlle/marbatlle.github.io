---
title: Basic Concepts Project
---

# Basic Concepts Project

### Actors Database

Teacher: Carlos González Calvo (carlosgo@ucm.es)


Practice project for the final evaluation of the Python lesson

#### Exercice 1
We want to store the data of our favorite actors in a database (BBDD), but we don't like any of the available ones, therefore we are going to build it ourselves.


The DB will be a dictionary of dictionaries. For the first dictionary the key will be the name of the actor. The second dictionary (the one that would be inside the first dictionary) consists of 3 fields: year of birth, sex and a list with the name of the films in which you have participated.


The program will allow us to do a series of things, chosen from a menu:

1. Exit the program.
2. Enter the data of a new actor or actress (the number of films may vary from one actor to another) (if the actor already existed in the database, the data will be overwritten).
3. List all the actors showing only their names (with a certain format).
4. Show the data of a certain actor or actress (with a certain format).
5. Search for those actors whose year of birth is in a certain range of years (which will be asked from the user).
6. Find those actors of a certain sex.
7. Find those actors who have participated in a movie.


#### Exercice 2
Repeat the previous exercise but using functions. At a minimum, a function must be created to display the menu and collect the option chosen by the user, and a function for each option that encapsulates the actions that are performed in each particular option (as parameters, they must receive at least the DB). Additionally, functions can be created to display the database or part of it with a certain format on the screen.


#### Exercice 3
In order not to lose the data that the user is entering, we are going to store the database in a file called 'actors.txt'. In this way, each time the program is executed, the previously stored data must be recovered and when exiting the program the information from the database must be written to a file.

https://github.com/marbatlle/Basic_Python_Project


*If you cannot access the github repository, please contact me so I can share it!*
