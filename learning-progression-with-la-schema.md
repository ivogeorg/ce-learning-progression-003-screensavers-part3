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

- what is a library?  
- how does this actually get into MakeCode?  
- what are these annotations?  
- what other files does it depend on?  

##### enum types

- `Direction`  
- `LedSpriteProperty`  

##### Namespace `game`

- functions
  - exported  
  - non-exported?  (if not, show another library)  
- classes  
- comments!!!  

##### Exported functions

- `createSprite`  
- game-related  

##### Class `LedSprite`

[`game.ts`](https://github.com/microsoft/pxt-microbit/blob/master/libs/core/game.ts)  
   - export  
   - functions (`createSprite`)  
   - classes (`LedSprite`)  
   - namespaces (`game`)  
   - use of variables  
   - TODO:
     - micro:bit [tech docs](https://makecode.com/docs)  
     - TS [namespaces](https://www.typescriptlang.org/docs/handbook/namespaces.html)  

#### 2. Apply
[[toc](#table-of-contents)]

1. `[<lernact-prac>]`Organize your screensavers program like the [`game.ts` library](https://github.com/microsoft/pxt-microbit/blob/master/libs/core/game.ts) and write the main program at the very bottom. 
2. `[<lernact-prac>]`For each global variable, function, and class method, write a descriptive comment, on the side of the variables and on top for the functions/methods. Remember the _last repository commit_ of this process.    

#### 3. Present
[[toc](#table-of-contents)]

In the [programs](programs) directory:
1. Add your program from 9.2.1 with filename `microbit-program-9-2-1.js`.  
2. Add your program from 9.2.2 with filename `microbit-program-9-2-2.js`.  

In the [Lab Notebook](README.md):
1. Link to the program from 9.2.1.  
2. Link to a demo video showing the execution of the program from 9.2.1.  
3. Link to the program from 9.2.2.  
4. Link to a demo video showing the execution of the program from 9.2.2.  

   
### 10. Iterative development with Github  
[[toc](#table-of-contents)]

#### 1. Study
[[toc](#table-of-contents)]

##### Git command line

##### Git remote and local

##### Git commands

- init  
- clone  
- status
- add  
- commit  
  - informative messages  
- pull  
- push

- creating directories  
  - no empty directories, so add `empty.txt` (`touch`)  
  - adding images  
- mv, rm, cp  

##### Github workflow

- markdown (README.md)    
- branching & merging  
- pull requests (strictly Github, not Git)  
- Github Classroom piggy-backing on Pull Requests for **Feedback**  
- releases & tags  

##### Incremental development

- incremental development examples:
  - `Complex` class live declaration and incremental development  
  - `UnsignedBinary` class live declaration and incremental development  
- [tag_example](https://github.com/ivogeorg/ce-learning-progression-002-bouncing-sprites/releases/tag/v1.0)  
  - record taking the current state of the `Complex` code and tagging it  
  - record taking the current state of the `UnsignedBinary` code and tagging it  

#### 2. Apply
[[toc](#table-of-contents)]

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

- Advanced material: [software stack](https://mattwarren.org/2017/11/28/Exploring-the-BBC-microbit-Software-Stack/)  
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

