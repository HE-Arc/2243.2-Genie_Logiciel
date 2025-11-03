---
title: "7 - Introduction à CMake et Ninja"
type: docs
weight: 10
---
# Chapitre 7 : Introduction à CMake et Ninja

## Slides

{{< pdf src="/pdfs/2243.2_07_IntroCMakeEtNinja.pdf" >}}

## Exercices

### Exercice 0 : mise en place
Créer un répertoire de travail (**`/Hello_CMake`** par exemple) et recopier les fichiers suivants en respectant la structure des dossiers :

**`/CMakeLists.txt`**
```bash
###############################################################################
##########          MINIMUM REQUIREMENTS (some need to be BEFORE project command)
###############################################################################

###############################################################################
##########          PROJECT DETAILS
###############################################################################
cmake_minimum_required(VERSION 3.16)
project(Hello_CMake)

###############################################################################
##########          REQUIREMENTS + GLOBAL DEFINITION
###############################################################################

###############################################################################
##########          PLATFORM SPECIFIC GLOBAL SETTINGS
###############################################################################

###############################################################################
##########          INTERNAL PROJECTS (OUR OWN)
###############################################################################
add_subdirectory(Hello)
add_subdirectory(World)

# Declares an executable called 2242.1_Main containing file main.cpp
add_executable(2242.1_Main main.cpp)

# Specifies that Main executable depends on libraries 2242.1_Hello 2242.1_World
target_link_libraries(2242.1_Main 2242.1_Hello 2242.1_World)
```

**`/main.cpp`**
```cpp
#include "Hello/Hello.h"
#include "World/World.h"

#include <iostream>

int main()
{
	Hello hello;
	World world;

	hello.Run();
	world.Run();

	return 0;
}
```

**`/Hello/CMakeLists.txt`**
```bash
###############################################################################
##########          MINIMUM REQUIREMENTS (some need to be BEFORE project command)
###############################################################################

###############################################################################
##########          REQUIREMENTS + GLOBAL DEFINITION
###############################################################################

###############################################################################
##########          PLATFORM SPECIFIC GLOBAL SETTINGS
###############################################################################

###############################################################################
##########          INTERNAL PROJECTS (OUR OWN)
###############################################################################
# Declares a library called 2242.1_Hello containing files Hello.h and Hello.cpp
add_library(2242.1_Hello Hello.cpp Hello.h)
```

**`/Hello/Hello.h`**
```cpp
#pragma once

class Hello
{
public:

	Hello() = default;
	virtual ~Hello() = default;
	Hello(const Hello &hello) = delete;
	Hello &operator=(const Hello &hello) = delete;

	void Run();
};
```

**`/Hello/Hello.cpp`**
```cpp
// STD
#include <iostream>
// LOCAL INCLUDES
#include "Hello.h"

void Hello::Run()
{
	std::cout << "Hello";
}
```

**`/World/CMakeLists.txt`**
```bash
###############################################################################
##########          MINIMUM REQUIREMENTS (some need to be BEFORE project command)
###############################################################################

###############################################################################
##########          REQUIREMENTS + GLOBAL DEFINITION
###############################################################################

###############################################################################
##########          PLATFORM SPECIFIC GLOBAL SETTINGS
###############################################################################

###############################################################################
##########          INTERNAL PROJECTS (OUR OWN)
###############################################################################
# Declares a library called 2242.1_World containing files World.h and World.cpp
add_library(2242.1_World World.cpp World.h)
```

**`/World/World.h`**
```cpp
#pragma once

class World
{
public:

	World() = default;
	virtual ~World() = default;
	World(const World &world) = delete;
	World &operator=(const World &world) = delete;

	void Run();
};
```

**`/World/World.cpp`**
```cpp
// STD
#include <iostream>
// LOCAL INCLUDES
#include "World.h"

void World::Run()
{
	std::cout << " World!!!" << std::endl;
}
```

### Exercice 1 - Exécuter CMake et Ninja en local
1. Installer [CMake](https://cmake.org/download/) et [Ninja](https://ninja-build.org/) sur votre machine si ce n'est pas déjà fait.
2. Suivre les instructions données durant le cours pour configurer et compiler un projet simple avec CMake et Ninja.

### Exercice 2 - Comprendre le fonctionnement de CMake
- Que se passe-t-il quand on modifie un fichier et qu'on recompile le projet ?
- Que se passe-t-il pour le fichiers compilés précédemment ?
