# CPE 1040 - Fall 2020

This is learning progression 003 for the Fall 2020 installment of the course CPE 1040: Introduction to Computer Engineering at MSU Denver.

Table of Contents
=================

* [CPE 1040 \- Fall 2020](#cpe-1040---fall-2020)
  * [Learning Progression 003: Screensavers (Part 3)](#learning-progression-003-screensavers-part-3)
    * [9\. Code reading](#9-code-reading)
      * [1\. Study](#1-study)
        * [game\.ts](#gamets)
        * [enum types](#enum-types)
        * [Namespace game](#namespace-game)
        * [Exported functions](#exported-functions)
        * [Class LedSprite](#class-ledsprite)
      * [2\. Apply](#2-apply)
      * [3\. Present](#3-present)
    * [10\. Iterative development with Github](#10-iterative-development-with-github)
      * [1\. Study](#1-study-1)
        * [Git command line](#git-command-line)
        * [Git remote and local](#git-remote-and-local)
        * [Git commands](#git-commands)
        * [Github workflow](#github-workflow)
        * [Incremental development](#incremental-development)
      * [2\. Apply](#2-apply-1)
      * [3\. Present](#3-present-1)
    * [11\. Reactive system](#11-reactive-system)
      * [1\. Study](#1-study-2)
        * [Software stack](#software-stack)
        * [Fiber scheduling](#fiber-scheduling)
        * [Registrant functions](#registrant-functions)
        * [forever vs while](#forever-vs-while)
      * [2\. Apply](#2-apply-2)
      * [3\. Present](#3-present-2)
    * [12\. Matrix dynamics](#12-matrix-dynamics)
      * [1\. Study](#1-study-3)
        * [Out\-of\-bound coordinates](#out-of-bound-coordinates)
        * [Smooth graphics](#smooth-graphics)
        * [Speed and scheduling](#speed-and-scheduling)
        * [Mod\-based timing](#mod-based-timing)
        * [Frame\-based display](#frame-based-display)
        * [Simulator fidelity revisited](#simulator-fidelity-revisited)
      * [2\. Apply](#2-apply-3)
      * [3\. Present](#3-present-3)

## Learning Progression 003: Screensavers (Part 3)
[[toc](#table-of-contents)]

This progression is the culmination of the first part of the course, in which we program the bear-bones micro:bit without any extenral circuitry attached and without communication features. We pull together all the programming language features and best practices that we introduced in the previous two learning progressions, to write a significantly larger target program over 12 steps. This will present the opportunity to learn about some of the design considerations a programmer makes when approaching a larger project. The progression is also going to dig a bit deeper into the _softare stack_ of the micro:bit, and uncover the ways it affects these considerations.
   
### 9. Code reading
[[toc](#table-of-contents)]

#### 1. Study
[[toc](#table-of-contents)]

##### game.ts

`[<lernact-rd>]`Being able to read programming code written by others is almost as important a skill as being able to write it yourself. This skill is called upon much more frequently than a novice programmer might expect. Large programming projects are highly collaborative undertakings and reading each other's code is one of the main activities of the project members.

Having the micro:bit as our model computer and MakeCode as our programming environment and editor, we will take [`game.ts`](https://github.com/microsoft/pxt-microbit/blob/master/libs/core/game.ts), one of the `[<cept>]`_library_ files of the Microsoft PXT project, the foundation for MakeCode's support for the micro:bit, as our object of exercise in code reading. This library defines the `game` namespace, which we have used when we used the `game.LedSprite` class in some programming tasks.

A library is a self-contained collection of programming artifacts, in particular `[<cept>]`_type definitions_, `[<cept>]`_functions_, and `[<cept>]`_classes_, generally of a common theme. A library has no `[<cept>]`_main program_, but instead is used as an already prepared resource in writing a main program. A libary exports (some of) its programming artifacts to be used in writing other libraries or standalone programs.

The way MakeCode exposes libraries like [`game.ts`](https://github.com/microsoft/pxt-microbit/blob/master/libs/core/game.ts) is by compiling all of them together in the TypeScript `[<cept>]`_runtime_. The TS runtime is a top layer of the micro:bit `[<cept>]`_software stack_. (If we instead wrote our programs in MicroPython, its runtime would be the top layer of the stack.) A runtime is a set of programs which translates human-readable programs in a particular programming language into a lower layer of software stack, which is usually much closer to the particular physical device that will run the programs. For example, in the case of the micro:bit, the layer below the TS runtime is the [micro:bit runtime](https://tech.microbit.org/software/runtime-mbed/), which abstracts the low-level functionality of the physical device into generic-device programming artifacts. For this reason, it is also called a `[<cept>]`_device abstraction layer_ (DAL). See the diagram showing the software stack of the micro:bit when we use TS to program it: 

<img src="images/microbit-software-stack-01.png" alt="micro:bit software stack sketch" width="600" />

The TS runtime is used in the in-browser MakeCode editor and simulator, but is also inserted as part of the generated HEX file that is written to the micro:bit device. You may notice that the comments above the programming artifacts included in the [`game.ts`](https://github.com/microsoft/pxt-microbit/blob/master/libs/core/game.ts) library are highly structured and look like code themselves. These are called `[<cept>]`_annotations_ and are used for various purposes, including presentation, linking in a programming environment, documentation generation, etc. The MakeCode editor, which presents artifacts in both Blocks and TS, these annotations are an inseparable part of creating such a straightforward programming environment. 

When we said that the [`game.ts`](https://github.com/microsoft/pxt-microbit/blob/master/libs/core/game.ts) library is self-contained, this was meant to mean that it defines the game package in its entirety. That is, there aren't two different libraries that have to be used in tandem to create a game for the micro:bit. This said, the library itself depends on artifacts defined in other libraries.

##### enum types

The [`game.ts`](https://github.com/microsoft/pxt-microbit/blob/master/libs/core/game.ts) library defines two enumerated (that is, `enum`) types:
1. `Direction` is used to simplify the manipulation of the `LedSprite` motion.    
2. `LedSpriteProperty` exposes 5 different "properties" of the `LedSprite`, creating a common mechanism for their retrieval and manipulation (aka getting and setting), as shown in the next example:
```javascript
// Example 9.1.1

let sprite : game.LedSprite = game.createSprite(4, 0)

let b : number = sprite.get(LedSpriteProperty.Brightness)  

sprite.set(LedSpriteProperty.Brightness, b/2)
```

An enumerated type is a programming artifact which has attributed of arrays and classes at the same time, though it is neither. It is multi-valued like an array, and it defines a type like a class. It is an ordered collection of names, which in themselves correspond to integers. All names can have their numeric value assigned explicitly, or they take the incremented value of the previous name in the collection:
```javascript
// Example 9.1.2

enum Value { Steel = 100, Silver = 250, Gold = 350 }
enum Bird { Sparrow = 0, Hawk, Eagle, Finch, Osprey, Canary }  // e.g. Bird.Finch equals 3
```

Notice that the two enumerated types are defined _outside_ the namespace `game`. Thus, they can be used freely for other purposes than the ones in defining a game environment. It is conventional to put types in the top-level scope of a program (or, in this case, library).

##### Namespace `game`

A namespace is a named scope (aka block):
```javascript
// Example 9.1.3

namespace screensaver { }
```
It is just a way to enclose a set of tightly related programming artifacts together. Those of the artifacts that are expected to be called from outside the scope are `[<cept>]`_exported_ via the keyword `export` put in front of the artifact signature. The `game` namespace exports game-related functions (e.g. `createSprite`) and the class `LedSprite`. As we have seen, this means we have to use the namespace name as a `[<cept>]`_prefix_ to the function and class names:
```javascript
// Example 9.1.4

let s : game.LedSprite = game.createSprite(2, 1)
```

The scope that a namespace provides is ideal for defining namespace-global variables for the specific purpose of the namespace (in our case, a micro:bit game) without contaminating the top-level program scope with them. The following example lists all the variables used in a game, which are nonetheless not directly visible to the programmer using the `game` package in MakeCode:
```javascript
// Example 9.1.4

namespace game {
    let _score: number = 0;
    let _life: number = 3;
    let _startTime: number = 0;
    let _endTime: number = 0;
    let _isGameOver: boolean = false;
    let _countdownPause: number = 0;
    let _level: number = 1;
    let _gameId: number = 0;
    let _img: Image;
    let _sprites: LedSprite[];
    let _paused: boolean = false;
    let _backgroundAnimation = false; // indicates if an auxiliary animation (and fiber) is already running
    
    // rest of the namespace
}
```
Reading through the namespace code, we see that these are the variables used internally by the functions in the namespace. Notice that the names all start with an _underscore_ (e.g. `_score`, _gameId_, etc.). This is a convention in programming for _internal_ variables that are not exposed and/or exported.

##### Exported functions

The functions declared in the `game` have to do with game-related functionality (e.g. `addScore`, `startCountdown`, `gameOver`, etc.). Most of them are exported and are meant to be used together. Most of the function names are self-explanatory, but, if in doubt, read the [reference](https://makecode.microbit.org/reference/game) for `game`.

Not all of the artifacts declared in the namespace need be exported. For example, the functions `checkStart`, `unplugEvents`, `init`, and `plot` are not exported, but are only used internally by exported functions.

##### Class `LedSprite`

We have already used the class `game.LedSprite`, for example, in `HaloSprite` where we `[<cept>]`_extended_ the base `game.LedSprite` class to add a halo around a bouncing sprite. One implementation of the `Raindrop` class can also use `game.LedSprite` as a `[<cept>]`_base class_. One obstacle for using it for all the screensavers is that every `game.LedSprite` is managed by the machinery of the `game` namespace, which has its own constraints and proper intended uses. For example, to remove a `game.Sprite` completely, one needs to explicitly call `delete()` on a sprite. Also, `game.LedSprite` objects do not accept out-of-bound coordinate values.

`game.LedSprite` is built on top of the much simpler functionality of turning LEDs on and off, and varying their brightness. For some of our screensavers, using `game.LedSprite` may make the implementation unnecessarily burdensome, because, like every data type defined by a class, there is a specific intended manner of manipulating objects of the type. For example, creating a new class `Raindrop` without extending `game.LedSprite` results in a much cleaner and shorter implementation.


#### 2. Apply
[[toc](#table-of-contents)]

1. `[<lernact-prac>]`Organize your `screensaver` namespace like the [`game.ts` library](https://github.com/microsoft/pxt-microbit/blob/master/libs/core/game.ts) library. Write the _main program_ at the very bottom, using the exported functions. _Do you have types outside the namespace? Do you need to export any classes?_   
2. `[<lernact-prac>]`For each global variable, function, and class method in the namespace `screensaver`, write a descriptive comment, on the side of the variables and on top for the functions/methods. Remember the _last repository commit_ of this process.    

#### 3. Present
[[toc](#table-of-contents)]

In the [programs](programs) directory:
1. Add your program from 9.2.1 with filename `microbit-program-9-2-1.js`.  
2. Add your program from 9.2.2 with filename `microbit-program-9-2-2.js`.  

In the [Lab Notebook](README.md):
1. Answer the questions in 9.2.1.  
2. Link to the program from 9.2.1.  
3. Link to a demo video showing the execution of the program from 9.2.1. This is needed as a verification that you haven't broken your code.  
4. Link to the program from 9.2.2.  
5. Link to a demo video showing the execution of the program from 9.2.2. This is needed as a verification that you haven't broken your code.  

   
### 10. Iterative development with Github  
[[toc](#table-of-contents)]

#### 1. Study
[[toc](#table-of-contents)]

##### Git command line

`[<lernact-rd>]`Github is built around the `[<cept>]`_version-control system_ [Git](https://git-scm.com/) (aka `[<cept>]`_source-control management_ system). The term "source" is used for the raw human-readable form of a program, to be contrasted against the machine-executable form of the program. Nowadays, no programming or engineering project is undertaken without keeping a dynamic record of all the changes made. As a large project does not happen overnight, this record is indispensable. It is the central component of modern engineering workflows, supporting a large range of team organizations, company policies, development use cases, and release schedules.  

One of the first large `[<cept>]`_open-source_ projects, and still one of the most popular, is the [Linux kernel](https://en.wikipedia.org/wiki/Linux_kernel), which is the basis for all Linux-based `[<cept>]`_operating systems_. Git was developed to coordinate its highly-distributed multi-person development. Just take a look at the number of commits to Linus Torvalds' [Linux kernel repository on Github](https://github.com/torvalds/linux) to get an idea of the scope of the project and the complexity of its maintenance.

This step asks you to install the `[<cept>]`_command-line_ [Git client](https://git-scm.com/), a program which can work with remote servers where Git repositories are maintained. Github is the largest such server. 

##### Git remote and local

We are already working with Git. You are reading a Markdown file in a private repostory which is owned the course staff and was created specifically for you. You have been added as an `[<cept>]`_outside collaborator_ and given full member access to the repository. You can create files, modify files, and make comments.

Working directly with the Github website, we are using Git only _indirectly_, because all Git operations are handled for us by Github. To learn Git, we need to take our code out of Github for a bit, and look at the underlying Git operations performed on it.

scenarios  

`git-repos`

commits  

##### Git commands

- init  
- clone  
- remote  
- status  
- add  
- commit  
  - informative commit messages  
- pull  
- push  

- creating directories  
  - no empty directories, so add `empty.txt` (`touch`)  
  - adding images  
- mv, rm, cp  

What Git commands each action we do on Github translates to.  

##### Github workflow

- markdown (README.md)   
- comments  
- branching & merging  
- pull requests (strictly Github, not Git)  
- Github Classroom piggy-backing on Pull Requests for **Feedback**  
- releases & tags  

##### Incremental development

- incremental development examples:
  - `class Complex` [video](https://msudenver.yuja.com/V/Video?v=1978529&node=7604592&a=1823805177&autoplay=1) and [code](https://gist.github.com/ivogeorg/842c36004e50143b43c6affd0dfa7984)    
  - `class UnsignedBinary` [video](https://msudenver.yuja.com/V/Video?v=1978655&node=7604844&a=1873218802&autoplay=1) and [code](https://gist.github.com/ivogeorg/ef5f46b8ca67cfa5cdf9c8cbd217c9ef)   
- [tag_example](https://github.com/ivogeorg/e-learning-progression-002-bouncing-sprites/releases/tag/v1.0)  

#### 2. Apply
[[toc](#table-of-contents)]

**TODO: Extra exercises**  
[Github Guides](https://guides.github.com/)  
1. `[<lernact-prac>]`Tag the last commit from 9.3.1 as `v0.8`. _Note: It should include your entries in the Lab Notebook._   
2. `[<lernact-prac>]`Tag the last commit from 9.3.1 as `v0.9`. _Note: It should include your entries in the Lab Notebook._  
3. `[<lernact-prac>]`Create a file `screensavers.js` from the `v0.9` program. Tag as `v1.0`.  

#### 3. Present
[[toc](#table-of-contents)]
   
In the [programs](programs) directory:
1. Add your program from 10.2.3 with filename `screensavers.js`.  

In the [Lab Notebook](README.md):
1. Link to the `v0.8` tag.  
2. Link to the `v0.9` tag.  
3. Link to the `v1.0` tag.  


### 11. Reactive system  
[[toc](#table-of-contents)]

#### 1. Study
[[toc](#table-of-contents)]

##### Software stack

- [micro:bit software](https://tech.microbit.org/software/)  
- [software stack](https://mattwarren.org/2017/11/28/Exploring-the-BBC-microbit-Software-Stack/)  
  - TS runtime  
  - micro:bit runtime (aka DAL)  
  - mbed OS  
    - drivers  
    - processor development kit  
- **threads**, fibers, and the [fiber scheduler](https://lancaster-university.github.io/microbit-docs/advanced/)  
  - Issues of speed, memory, etc.  
  - Thread(fiber)-unsafety: Issues of non-deterministic splitting & rearrangement of code portions   
  - (Brendan) Does a time slice have to end for event handling to proceed?  


##### Fiber scheduling 

- [reactive system](https://makecode.microbit.org/device/reactive)  
- part of the micro:bit runtime (DAL)  
  - [header](https://github.com/lancaster-university/microbit-dal/blob/master/inc/core/MicroBitFiber.h)  
  - [source](https://github.com/lancaster-university/microbit-dal/blob/master/source/core/MicroBitFiber.cpp)  
  - **TODO: find the fiber calls in pxt**  
- threads  
- fibers  
- scheduling  

##### Registrant functions 

- registrant functions and funcion arguments  
- `basic`  
- `input`  
- etc.  
- Why you shouldn't have event handling in a `forever` loop  
- How is `pause` executed and what is affected (e.g. other repeated behavior, event handling, etc.)  
  - `pause()` should be avoided, especially with multiple `forever()` loops  
  - `pause` calls `fiber_sleep(ms);`, so depending on what that does and what a fiber is executing, and how fibers are assigned, pause may only be blocking one fiber and may or may not have implications on the global dynamics   
    - [micro:bit runtime docs](https://lancaster-university.github.io/microbit-docs/advanced/)  
    - [fiber-sleep package](https://github.com/jcoreio/fiber-sleep) (the `Fibre` object calls `yield`)   

##### `forever` vs `while`

`forever` function vs `while` loop  

feature | `forever` | `while`
-- | -- | --
condition | no | yes
`break` | no | yes
scheduling | yes | no
simulator fidelity | yes | no

#### 2. Apply
[[toc](#table-of-contents)]

**TODO: Experiments?**  
1. `[<lernact-prac>]`Create 6 separate `forever` loops, each one containing `showNumber()` with one of the numbers n = 1, 3, 5, 7, 9, 11, 13. Describe the behavior. Can you see all the numbers clearly?  
2. `[<lernact-prac>]`Modify the previous program to show the either n or n + 1 toggled by pressing button A. Describe the behavior. How soon do the numbers switch after you press the button?  
3. `[<lernact-prac>]`Modify the previous program, adding a random `pause()` between 300 and 1200 ms after `showNumber()`. Describe the behavior. Can you see the numbers our of order?   

#### 3. Present
[[toc](#table-of-contents)]
   
In the [programs](programs) directory:
1. Add your program from 11.2.1 with filename `microbit-program-11-2-1.js`.  
2. Add your program from 11.2.2 with filename `microbit-program-11-2-2.js`.  
3. Add your program from 11.2.3 with filename `microbit-program-11-2-3.js`.  

In the [Lab Notebook](README.md):
1. Link to the program from 11.2.1 and describe its behavior.  
2. Link to a demo video showing the execution of the program from 11.2.1.  
3. Link to the program from 11.2.2 and describe its behavior.  
4. Link to a demo video showing the execution of the program from 11.2.2.  
5. Link to the program from 11.2.3 and describe its behavior.  
6. Link to a demo video showing the execution of the program from 11.2.3.  

### 12. Matrix dynamics  
[[toc](#table-of-contents)]

#### 1. Study
[[toc](#table-of-contents)]

##### Out-of-bound coordinates

- with `led.plot` and `led.unplot`  
- not with `LedSprite` (identify code lines in `game.ts` or elsewhere restricting coordinates)  

##### Smooth graphics

- don't use `pause()`, `show*()` for smooth graphics  
  - fiber states and lifecycle  
- `clearScreen()`, if used sparingly, is okay (it's fast)  

##### Speed and scheduling

- why do we need `pause()` after `clearScreen()`?
  ```javascript
  while (true) {
      if (isHeart) {                                             
          basic.showIcon(IconNames.Heart)
      } else {
          basic.showIcon(IconNames.Butterfly)
      }
      basic.pause(100)
      basic.clearScreen()
      basic.pause(100)                             // THIS IS REQUIRED TO SEE THE ICON BLINK
  }
  ```

##### Mod-based timing
    
- mod-based timing  
  - `rain`  
  - `bouncing_marbles`  

##### Frame-based display
    
- _frame_-based display for speed and smoothness  
 - 3d array for `slytherin`  
 
##### Simulator fidelity revisited

- simulator vs device  
  - manual fine-tuning  
  - dependency on code complexity  
  - efficient vs inefficient code  

#### 2. Apply
[[toc](#table-of-contents)]

**TODO** This is probably the most challenging screensaver. Expand to include everything learned, systematically organized into a unified software engineering experience!  
1. `[<lernact-prac>]`Slytherin screensaver. Three levels:
   1. [1 step point] A single snake with wrap-around and self-curl, bright head, random motion, and `turnDelay`.  
   2. [1 + 5 extra step point] Multiple snakes, with different colors and random overlap.  
   3. [1 + 10 step points] A 15% chance for a biter, which slithers on top of others, and kills them on contact (with head). Random repopulation.
2. `[<lernact-prac>]`Integrate into `screensavers.js` and tag with `v1.2`.  

#### 3. Present
[[toc](#table-of-contents)]
   
In the [programs](programs) directory:
1. Add your program from 12.2.1 with filename `microbit-program-12-2-1.js`.  
2. Add your program from 12.2.2 with filename `microbit-program-12-2-2.js`.  

In the [Lab Notebook](README.md):
1. Link to the program from 12.2.1.  
2. Link to a demo video showing the execution of the program from 12.2.1.  
3. Link to the program from 12.2.2.  
4. Link to a demo video showing the execution of the program from 12.2.2.  

