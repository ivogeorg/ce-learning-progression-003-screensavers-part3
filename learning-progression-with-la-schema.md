# CPE 1040 - Fall 2020

This is learning progression 003 for the Fall 2020 installment of the course CPE 1040: Introduction to Computer Engineering at MSU Denver.


## Learning Progression 003: Screensavers (Part 1)
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



#### 3. Present
[[toc](#table-of-contents)]

   
### 10. Iterative development with Github  
[[toc](#table-of-contents)]

#### 1. Study
[[toc](#table-of-contents)]

##### Git command line

##### Git remote and local

##### Git commands

- init  
- status
- add  
- commit  
  - informative messages  
- pull  
- push

##### Github workflow

- branches & merging  
- pull requests (strictly Github)  
- Github Classroom **Feedback**)  
- releases & tags  

##### Incremental development

- incremental development example  

#### 2. Apply
[[toc](#table-of-contents)]


#### 3. Present
[[toc](#table-of-contents)]
   

### 11. Reactive system  
[[toc](#table-of-contents)]

#### 1. Study
[[toc](#table-of-contents)]

`forever` function vs `while` loop  
feature | `forever` | `while`
-- | -- | --
condition | no | yes
`break` | no | yes
scheduling | yes | no
simulator fidelity | yes | no

    - [reactive system](https://makecode.microbit.org/device/reactive)  
    - Why you shouldn't have event handling in a `forever` loop  
    - How is `pause` executed and what is affected (e.g. other repeated behavior, event handling, etc.)  
      - `pause()` should be avoided, especially with multiple `forever()` loops  
    - Advanced material: [software stack](https://mattwarren.org/2017/11/28/Exploring-the-BBC-microbit-Software-Stack/)  
      - **threads**, fibers, and the [fiber scheduler](https://lancaster-university.github.io/microbit-docs/advanced/)  
      - Issues of speed, memory, etc.  
      - Thread(fiber)-unsafety: Issues of non-deterministic splitting & rearrangement of code portions   
      - (Brendan) Does a time slice have to end for event handling to proceed?  

#### 2. Apply
[[toc](#table-of-contents)]
#### 3. Present
[[toc](#table-of-contents)]
   

### 12. Matrix dynamics  
[[toc](#table-of-contents)]

#### 1. Study
[[toc](#table-of-contents)]

    - can use out-of-bound coordinates in `plot()` and `unplot()`  
    - don't use `pause()`, `show*()` for smooth graphics 
    - `clearScreen()` is often necessary but it's fast, so no problem  
    - why do we need `pause()` after `clearScreen()`?
      ```javascript
      while (true) {
          if (isHeart)                                             
              basic.showIcon(IconNames.Heart)
          else
              basic.showIcon(IconNames.Butterfly)
          basic.pause(100)
          basic.clearScreen()
          basic.pause(100)                             // THIS IS REQUIRED TO SEE THE ICON BLINK
      }
      ```
    - _frame_-based display for speed and smoothness  
    - mod-based timing  
      - simulator vs device  
      - fine-tuning

#### 2. Apply
[[toc](#table-of-contents)]
#### 3. Present
[[toc](#table-of-contents)]
   

