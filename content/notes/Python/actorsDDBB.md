---
title: ""
linktitle: Basic Concepts Project
toc: true
type: docs
date: "2019-05-05T00:00:00+01:00"
draft: false
menu:
  example:
    parent: Python
    weight: 2

# Prev/next pager order (if `docs_section_pager` enabled in `params.toml`)
weight: 2
---

<center><b><font color='DARKRED' size='4px'>MSc. Personalized Medicine and Health Applied Bioinformatics</font></b></center>



# <font color='FIREBRICK'>Python Final Project</font>

<font size='2px'><p style="text-align: justify;line-height: 150%">Practice project for the final evaluation of the Python lesson</p></font>

## <font color='FIREBRICK'>Exercice 1</font>

<font size='1px'><p style="text-align: justify;line-height: 150%"><font size='2px'><p style="text-align: justify;line-height: 150%">Exercice 1
We want to store the data of our favorite actors in a database (BBDD), but we don't like any of the available ones, therefore we are going to build it ourselves.
The DB will be a dictionary of dictionaries. For the first dictionary the key will be the name of the actor. The second dictionary (the one that would be inside the first dictionary) consists of 3 fields: year of birth, sex and a list with the name of the films in which you have participated.
The program will allow us to do a series of things, chosen from a menu:

1. Exit the program.
2. Enter the data of a new actor or actress (the number of films may vary from one actor to another) (if the actor already existed in 4. the database, the data will be overwritten).
3. List all the actors showing only their names (with a certain format).
4. Show the data of a certain actor or actress (with a certain format).
5. Search for those actors whose year of birth is in a certain range of years (which will be asked from the user).
6. Find those actors of a certain sex.
7.Find those actors who have participated in a movie.


```python
# Creación del Diccionario Vacío

BBDD_actores = {}

# Creación Menú
print("BIENVENIDO A LA BBDD DE ACTORES")
while True :
    # Mostrar el menú por pantalla
    print("\n\nMENU DE LA BBDD-ACTORES\n",
          "\n1) Salir del programa",
          "\n2) Introducir los datos de un nuevo actor o actriz",
          "\n3) Listar todos los actores mostrando únicamente sus nombres",
          "\n4) Mostrar los datos de un determinado actor o actriz",
          "\n5) Buscar aquellos actores cuyo año de nacimiento se encuentre en un determinado rango de años",
          "\n6) Buscar aquellos actores de un sexo determinado",
          "\n7) Buscar aquellos actores que hayan participado en una película\n\n")
    while True:
        input_menu = input("\nElija una opción del menú: ")
        try:
            opcion = int(input_menu)
            if opcion in list(range(1,8)):
                break
            else:
                print("Porfavor, introduzca un valor del 1 al 7")
        except ValueError:
            print("Porfavor, introduzca un número entero") 
        
    # si la opción es la 1
    if opcion == 1 :
        # Salir del programa
        print("\nSALIDA DE LA BBDD COMPLETADA\n\n¡Hasta la vista!")
        break   
        
    # sino, si la opción es la 2
    elif opcion == 2 :
        # Introducir los datos de un nuevo actor o actriz
        ## nombre
        input_nombre = input("Introduzca el nombre del actor o la actriz: ")
        ## año de nacimiento
        while True:
            input_nacimiento = input("Introduzca su año de nacimiento: ")
            try:
                nacimiento_integer = int(input_nacimiento)
                break
            except ValueError:
                print("Porfavor, introduzca un número entero") 
        ## sexo
        while True:
            input_sexo = input("Introduzca su genero (M o F): ")
            if input_sexo != 'M' and input_sexo != 'F':
                print("Porfavor, introduzca M o F")
            else: 
                break
        ## películas
        if input_nombre in BBDD_actores:
            lista_peliculas = BBDD_actores[input_nombre]['peliculas']
        else:
            lista_peliculas = []
        print("\nIntroduzca las películas donde ha participado: ",
                  "\n(Para finalizar introduzca fin)")
        while True:
            pelicula = input()
            if pelicula == 'fin':
                break
            elif pelicula not in lista_peliculas:
                lista_peliculas.append(pelicula)
            else:
                continue    
        BBDD_actores[input_nombre] = {}
        BBDD_actores[input_nombre]['año'] = nacimiento_integer
        BBDD_actores[input_nombre]['sexo'] = input_sexo
        BBDD_actores[input_nombre]['peliculas'] = lista_peliculas
        
    # sino, si la opción es la 3
    elif opcion == 3 :
        # Listar todos los actores mostrando únicamente sus nombres
        nombres_lista = [key for key in BBDD_actores.keys()]
        if not nombres_lista:
            print("Su base de datos se encuentra vacía")
        else: 
            print("\nActores y actrices en la BBDD: ",", ".join(nombres_lista) + ".\n")
        
        
    # sino, si la opción es la 4
    elif opcion == 4 :
        # Mostrar los datos de un determinado actor o actriz
        while True:
            input_actor = input("Nombre del actor o actriz: ")
            if input_actor in BBDD_actores:
                if BBDD_actores[input_actor]['sexo'] == 'M':
                    print("\nInformación sobre el actor: ", input_actor, 
                          "nació el año" , BBDD_actores[input_actor]['año'],
                          "y su filmografía incluye:", ", ".join(BBDD_actores[input_actor]['peliculas'])+".\n")
                else:
                    print("\nInformación sobre la actriz: ", input_actor, 
                          "nació el año" , BBDD_actores[input_actor]['año'],
                          "y su filmografía incluye:", ", ".join(BBDD_actores[input_actor]['peliculas'])+".\n")
                break
            else:
                print("\nNo hemos encontrado este actor o actriz en nuestra base de datos\n")
                while True:
                    error = input("Quieres introducir otro nombre? ").lower()
                    if error == 'no' or error == 'si' or error == 'sí':
                        break
                    else:
                        print("ERROR. Responde sí o no","\n")
                        continue
                if error == 'no':
                    break
                if error == 'si' or error == 'sí':
                    continue
        
    # sino, si la opción es la 5
    elif opcion == 5 :
        # Buscar aquellos actores cuyo año de nacimiento se encuentre en un determinado rango de años
        edad_maxima = int(input("Buscar actores nacidos después del año: "))
        edad_minima = int(input("Pero antes del año: "))
        actores_rango = []
        for nombre in BBDD_actores.keys():
            if BBDD_actores[nombre]["año"] in list(range(edad_maxima + 1, edad_minima)):
                actores_rango.append(nombre)
        print("\nActores nacidos después de año", str(edad_maxima), 
              "y antes del", str(edad_minima) + ":", ", ".join(actores_rango) + ".\n")
        
    # sino, si la opción es la 6
    elif opcion == 6 :
        # Buscar aquellos actores de un sexo determinado
        while True:
            input_sexo = input("Buscar M o F?: ")
            if input_sexo == 'M':
                actores_M = []
                for nombre in BBDD_actores.keys():
                    if BBDD_actores[nombre]["sexo"] == 'M':
                        actores_M.append(nombre)
                print("\nLista de actores en la BBDD:", ", ".join(actores_M) + ".\n")
                break
            elif input_sexo == 'F':
                actores_F = []
                for nombre in BBDD_actores.keys():
                    if BBDD_actores[nombre]["sexo"] == 'F':
                        actores_F.append(nombre)
                print("\nLista de actrices en la BBDD:", ", ".join(actores_F) + ".\n")
                break
            else: 
                print("\nError. Introduce M o F\n")

    # sino, si la opción es la 7
    elif opcion == 7 :
        # Buscar aquellos actores que hayan participado en una película
        while True:
            input_pelicula = input("Nombre de la pelicula: ")
            actores_pelicula = []
            for nombre in BBDD_actores.keys():
                if input_pelicula in BBDD_actores[nombre]['peliculas']:
                    actores_pelicula.append(nombre)
            if len(actores_pelicula) >= 1: 
                print("\nActor/es que aparecen en", input_pelicula, ":", ", ".join(actores_pelicula) + ".\n")
                break
            else:
                print("\nNingún actor de la BBDD aparece en la pelicula:", input_pelicula,"\n")
                while True:
                    error = input("Quieres introducir otra película? ").lower()
                    if error == 'no' or error == 'si' or error == 'sí':
                        break
                    else:
                        print("ERROR. Responde sí o no","\n")
                        continue
                if error == 'no':
                    break
                if error == 'si' or error == 'sí':
                    continue
```

## <font color='FIREBRICK'>Exercice 2</font>

<font size='1px'><p style="text-align: justify;line-height: 150%"><font size='2px'><p style="text-align: justify;line-height: 150%">Repeat the previous exercise but using functions. At a minimum, a function must be created to display the menu and collect the option chosen by the user, and a function for each option that encapsulates the actions that are performed in each particular option (as parameters, they must receive at least the DB). Additionally, functions can be created to display the database or part of it with a certain format on the screen.</p></font></p></font>


```python
# Creación Función Menú
def menu_BBDD():
    print("\n\nMENU DE LA BBDD-ACTORES\n",
          "\n1) Salir del programa",
          "\n2) Introducir los datos de un nuevo actor o actriz",
          "\n3) Listar todos los actores mostrando únicamente sus nombres",
          "\n4) Mostrar los datos de un determinado actor o actriz",
          "\n5) Buscar aquellos actores cuyo año de nacimiento se encuentre en un determinado rango de años",
          "\n6) Buscar aquellos actores de un sexo determinado",
          "\n7) Buscar aquellos actores que hayan participado en una película\n\n")
    while True:
        input_menu = input("\nElija una opción del menú: ")
        try:
            opcion = int(input_menu)
            if opcion in list(range(1,8)):
                break
            else:
                print("Porfavor, introduzca un valor del 1 al 7")
        except ValueError:
            print("Porfavor, introduzca un número entero") 
    return opcion

# Creación Función Opción 2
def opcion_2(BBDD_actores):
    input_nombre = input("Introduzca el nombre del actor o la actriz: ")
    while True:
        input_nacimiento = input("Introduzca su año de nacimiento: ")
        try:
            nacimiento_integer = int(input_nacimiento)
            break
        except ValueError:
            print("Porfavor, introduzca un número entero") 
    while True:
        input_sexo = input("Introduzca su genero (M o F): ")
        if input_sexo != 'M' and input_sexo != 'F':
            print("Porfavor, introduzca M o F")
        else: 
            break
    if input_nombre in BBDD_actores:
        lista_peliculas = BBDD_actores[input_nombre]['peliculas']
    else:
        lista_peliculas = []
    print("\nIntroduzca las películas donde ha participado: ",
              "\n(Para finalizar introduzca fin)")
    while True:
        pelicula = input()
        if pelicula == 'fin':
            break
        elif pelicula not in lista_peliculas:
            lista_peliculas.append(pelicula)
        else:
            continue
    BBDD_actores[input_nombre] = {}
    BBDD_actores[input_nombre]['año'] = nacimiento_integer
    BBDD_actores[input_nombre]['sexo'] = input_sexo
    BBDD_actores[input_nombre]['peliculas'] = lista_peliculas

# Creación Función Opción 3
def opcion_3(BBDD_actores):
    nombres_lista = [key for key in BBDD_actores.keys()]
    if not nombres_lista:
        print("Su base de datos se encuentra vacía")
    else: 
        print("\nActores y actrices en la BBDD: ",", ".join(nombres_lista) + ".\n")
                     
# Creación Función Opción 4
def opcion_4(BBDD_actores):
    while True:
        input_actor = input("Nombre del actor o actriz: ")
        if input_actor in BBDD_actores:
            if BBDD_actores[input_actor]['sexo'] == 'M':
                print("\nInformación sobre el actor: ", input_actor, 
                      "nació el año" , BBDD_actores[input_actor]['año'],
                      "y su filmografía incluye:", ", ".join(BBDD_actores[input_actor]['peliculas'])+".\n")
            else:
                print("\nInformación sobre la actriz: ", input_actor, 
                      "nació el año" , BBDD_actores[input_actor]['año'],
                      "y su filmografía incluye:", ", ".join(BBDD_actores[input_actor]['peliculas'])+".\n")
            break
        else:
            print("\nNo hemos encontrado este actor o actriz en nuestra base de datos\n")
            while True:
                error = input("Quieres introducir otro nombre? ").lower()
                if error == 'no' or error == 'si' or error == 'sí':
                    break
                else:
                    print("ERROR. Responde sí o no","\n")
                    continue
            if error == 'no':
                break
            if error == 'si' or error == 'sí':
                continue
                    
# Creación Función Opción 5
def opcion_5(BBDD_actores):
    edad_maxima = int(input("Buscar actores nacidos después del año: "))
    edad_minima = int(input("Pero antes del año: "))
    actores_rango = []
    for nombre in BBDD_actores.keys():
        if BBDD_actores[nombre]["año"] in list(range(edad_maxima + 1, edad_minima)):
            actores_rango.append(nombre)
    print("\nActores nacidos después de año", str(edad_maxima), 
          "y antes del", str(edad_minima) + ":", ", ".join(actores_rango) + ".\n")
        
        
# Creación Función Opción 6
def opcion_6(BBDD_actores):
    while True:
        input_sexo = input("Buscar M o F?: ")
        if input_sexo == 'M':
            actores_M = []
            for nombre in BBDD_actores.keys():
                if BBDD_actores[nombre]["sexo"] == 'M':
                    actores_M.append(nombre)
            print("\nLista de actores en la BBDD:", ", ".join(actores_M) + ".\n")
            break
        elif input_sexo == 'F':
            actores_F = []
            for nombre in BBDD_actores.keys():
                if BBDD_actores[nombre]["sexo"] == 'F':
                    actores_F.append(nombre)
            print("\nLista de actrices en la BBDD:", ", ".join(actores_F) + ".\n")
            break
        else: 
            print("\nError. Introduce M o F\n")
                
# Creación Función Opción 7
def opcion_7(BBDD_actores):
    while True:
        input_pelicula = input("Nombre de la pelicula: ")
        actores_pelicula = []
        for nombre in BBDD_actores.keys():
            if input_pelicula in BBDD_actores[nombre]['peliculas']:
                actores_pelicula.append(nombre)
        if len(actores_pelicula) >= 1: 
            print("\nActor/es que aparecen en", input_pelicula, ":", ", ".join(actores_pelicula) + ".\n")
            break
        else:
            print("\nNingún actor de la BBDD aparece en la pelicula:", input_pelicula,"\n")
            while True:
                error = input("Quieres introducir otra película? ").lower()
                if error == 'no' or error == 'si' or error == 'sí':
                    break
                else:
                    print("ERROR. Responde sí o no","\n")
                    continue
            if error == 'no':
                break
            if error == 'si' or error == 'sí':
                continue

# Creación del Diccionario Vacío y Bienvenida
BBDD_actores = {}
print("BIENVENIDO A LA BBDD DE ACTORES")

# Creación de Función de Funciones
while True:
    opcion = menu_BBDD()
    if opcion == 1:
        break
    elif opcion == 2:
        opcion_2(BBDD_actores)
    elif opcion == 3:
        opcion_3(BBDD_actores)
    elif opcion == 4:
        opcion_4(BBDD_actores)
    elif opcion == 5:
        opcion_5(BBDD_actores)
    elif opcion == 6:
        opcion_6(BBDD_actores)
    elif opcion == 7:
        opcion_7(BBDD_actores)
print("\nSALIDA DE LA BBDD COMPLETADA\n\n¡Hasta la vista!")
```

    BIENVENIDO A LA BBDD DE ACTORES
    
    
    MENU DE LA BBDD-ACTORES
     
    1) Salir del programa 
    2) Introducir los datos de un nuevo actor o actriz 
    3) Listar todos los actores mostrando únicamente sus nombres 
    4) Mostrar los datos de un determinado actor o actriz 
    5) Buscar aquellos actores cuyo año de nacimiento se encuentre en un determinado rango de años 
    6) Buscar aquellos actores de un sexo determinado 
    7) Buscar aquellos actores que hayan participado en una película
    
    


## <font color='FIREBRICK'>Exercice 3</font>

<font size='3px'><p style="text-align: justify;line-height: 150%"><font size='3px'><p style="text-align: justify;line-height: 150%">Repeat the previous exercise but using functions. At a minimum, a function must be created to display the menu and collect the option chosen by the user, and a function for each option that encapsulates the actions that are performed in each particular option (as parameters, they must receive at least the DB). Additionally, functions can be created to display the database or part of it with a certain format on the screen.</p></font></p></font>


```python
# Creación Funciones de la BBDD
def menu_BBDD_actores():
    print("\n\nMENU DE LA BBDD-ACTORES\n",
          "\n1) Salir del programa",
          "\n2) Introducir los datos de un nuevo actor o actriz",
          "\n3) Listar todos los actores mostrando únicamente sus nombres",
          "\n4) Mostrar los datos de un determinado actor o actriz",
          "\n5) Buscar aquellos actores cuyo año de nacimiento se encuentre en un determinado rango de años",
          "\n6) Buscar aquellos actores de un sexo determinado",
          "\n7) Buscar aquellos actores que hayan participado en una película\n\n")
    while True:
        input_menu = input("\nElija una opción del menú: ")
        try:
            opcion = int(input_menu)
            if opcion in list(range(1,8)):
                break
            else:
                print("Porfavor, introduzca un valor del 1 al 7")
        except ValueError:
            print("Porfavor, introduzca un número entero") 
    return opcion

def opcion_2(BBDD_actores):
    input_nombre = input("Introduzca el nombre del actor o la actriz: ")
    while True:
        input_nacimiento = input("Introduzca su año de nacimiento: ")
        try:
            nacimiento_integer = int(input_nacimiento)
            break
        except ValueError:
            print("Porfavor, introduzca un número entero") 
    while True:
        input_sexo = input("Introduzca su genero (M o F): ")
        if input_sexo != 'M' and input_sexo != 'F':
            print("Porfavor, introduzca M o F")
        else: 
            break
    if input_nombre in BBDD_actores:
        lista_peliculas = BBDD_actores[input_nombre]['peliculas']
    else:
        lista_peliculas = []
    print("\nIntroduzca las películas donde ha participado: ",
              "\n(Para finalizar introduzca fin)")
    while True:
        pelicula = input()
        if pelicula == 'fin':
            break
        elif pelicula not in lista_peliculas:
            lista_peliculas.append(pelicula)
        else:
            continue
    BBDD_actores[input_nombre] = {}
    BBDD_actores[input_nombre]['año'] = nacimiento_integer
    BBDD_actores[input_nombre]['sexo'] = input_sexo
    BBDD_actores[input_nombre]['peliculas'] = lista_peliculas

def opcion_3(BBDD_actores):
    nombres_lista = [key for key in BBDD_actores.keys()]
    if not nombres_lista:
        print("Su base de datos se encuentra vacía")
    else: 
        print("\nActores y actrices en la BBDD: ",", ".join(nombres_lista) + ".\n")
                     
def opcion_4(BBDD_actores):
    while True:
        input_actor = input("Nombre del actor o actriz: ")
        if input_actor in BBDD_actores:
            if BBDD_actores[input_actor]['sexo'] == 'M':
                print("\nInformación sobre el actor: ", input_actor, 
                      "nació el año" , BBDD_actores[input_actor]['año'],
                      "y su filmografía incluye:", ", ".join(BBDD_actores[input_actor]['peliculas'])+".\n")
            else:
                print("\nInformación sobre la actriz: ", input_actor, 
                      "nació el año" , BBDD_actores[input_actor]['año'],
                      "y su filmografía incluye:", ", ".join(BBDD_actores[input_actor]['peliculas'])+".\n")
            break
        else:
            print("\nNo hemos encontrado este actor o actriz en nuestra base de datos\n")
            while True:
                error = input("Quieres introducir otro nombre? ").lower()
                if error == 'no' or error == 'si' or error == 'sí':
                    break
                else:
                    print("ERROR. Responde sí o no","\n")
                    continue
            if error == 'no':
                break
            if error == 'si' or error == 'sí':
                continue
                    
def opcion_5(BBDD_actores):
    edad_maxima = int(input("Buscar actores nacidos después del año: "))
    edad_minima = int(input("Pero antes del año: "))
    actores_rango = []
    for nombre in BBDD_actores.keys():
        if BBDD_actores[nombre]["año"] in list(range(edad_maxima + 1, edad_minima)):
            actores_rango.append(nombre)
    print("\nActores nacidos después de año", str(edad_maxima), 
          "y antes del", str(edad_minima) + ":", ", ".join(actores_rango) + ".\n")
        
def opcion_6(BBDD_actores):
    while True:
        input_sexo = input("Buscar M o F?: ")
        if input_sexo == 'M':
            actores_M = []
            for nombre in BBDD_actores.keys():
                if BBDD_actores[nombre]["sexo"] == 'M':
                    actores_M.append(nombre)
            print("\nLista de actores en la BBDD:", ", ".join(actores_M) + ".\n")
            break
        elif input_sexo == 'F':
            actores_F = []
            for nombre in BBDD_actores.keys():
                if BBDD_actores[nombre]["sexo"] == 'F':
                    actores_F.append(nombre)
            print("\nLista de actrices en la BBDD:", ", ".join(actores_F) + ".\n")
            break
        else: 
            print("\nError. Introduce M o F\n")
                
# Creación Función Opción 7
def opcion_7(BBDD_actores):
    while True:
        input_pelicula = input("Nombre de la pelicula: ")
        actores_pelicula = []
        for nombre in BBDD_actores.keys():
            if input_pelicula in BBDD_actores[nombre]['peliculas']:
                actores_pelicula.append(nombre)
        if len(actores_pelicula) >= 1: 
            print("\nActor/es que aparecen en", input_pelicula + ":", ", ".join(actores_pelicula) + ".\n")
            break
        else:
            print("\nNingún actor de la BBDD aparece en la pelicula:", input_pelicula,"\n")
            while True:
                error = input("Quieres introducir otra película? ").lower()
                if error == 'no' or error == 'si' or error == 'sí':
                    break
                else:
                    print("ERROR. Responde sí o no","\n")
                    continue
            if error == 'no':
                break
            if error == 'si' or error == 'sí':
                continue
            
# Creación del Diccionario Vacío y Bienvenida
print("BIENVENIDO A LA BBDD DE ACTORES")
with open("Actors-DDBB.txt",'r') as BBDD:
    BBDD_actores = {}
    for actor in BBDD:
        lista_bbdd = actor.split(";")
        BBDD_actores[lista_bbdd[0]] = {}
        BBDD_actores[lista_bbdd[0]]['año'] = int(lista_bbdd[1])
        BBDD_actores[lista_bbdd[0]]['sexo'] = lista_bbdd[2]
        lista_peliculas = lista_bbdd[3].split(',')
        nueva_lista_peliculas = lista_peliculas[:-1]
        nueva_lista_peliculas.append(lista_peliculas[-1].replace('\n',''))
        BBDD_actores[lista_bbdd[0]]['peliculas'] = nueva_lista_peliculas

# Creación de Función de Funciones
while True:
    opcion = menu_BBDD_actores()
    if opcion == 1:
        with open("Actors-DDBB.txt", "w") as BBDD:
            for actor in BBDD_actores:
                nueva_entrada = actor + ";" + str(BBDD_actores[actor]['año']) + ";" + BBDD_actores[actor]['sexo'] + ";" + ",".join(BBDD_actores[actor]['peliculas'])
                nueva_entrada += "\n"
                BBDD.write(nueva_entrada)
            break
    elif opcion == 2:
        opcion_2(BBDD_actores)
    elif opcion == 3:
        opcion_3(BBDD_actores)
    elif opcion == 4:
        opcion_4(BBDD_actores)
    elif opcion == 5:
        opcion_5(BBDD_actores)
    elif opcion == 6:
        opcion_6(BBDD_actores)
    elif opcion == 7:
        opcion_7(BBDD_actores)
print("\nSALIDA DE LA BBDD COMPLETADA\n\n¡Hasta la vista!")
```

#### <center><font color='INDIANRED'>Autor: Carlos González Calvo (carlosgo@ucm.es)</font></center>
