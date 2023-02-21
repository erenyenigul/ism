<img src="docs/logo.png" alt=“ISM-logo” width="50">

# IOS Stack Machine

## Ever wondered if you can use Apple Notes to write code? 📝
(probably not.)
Well, now you can!

IOS Stack Machine (ISM) is an interpreter implemented in Apple Shortcuts, thus it works in all Apple devices that have Shortcuts app installed.
## Installation

To install ISM, directly download `IOS Stack Machine.shortcut` which is located in this repository. Shortcuts app may require you to change some settings. After adding IOS Stack Machine to your Shortcuts, you are good to go! 

Also, I heard that .shortcut files sometimes cause issues. So, you can also download the shortcut from [here](https://www.icloud.com/shortcuts/5e1d3ec5e1c6490d886556400ec01b3a).

## Quick Start: Hello World

After installing ISM to your device, go ahead and open Notes app and create a new note. The name of your note should end with `.ism`, so that ISM can see your code. That's why after naming your note, append `.ism`to the end of title.

To the next line, append this code.

```asm
println Hello world!
```
In ISM, every line must contain a single instruction. First word in the line is the instruction name and the rest is the arguments. Beware that number of spaces between each argument, or between argument and the instruction matters. There should be a single space.

Also, as you've seen, you don't need to use double quotes (`"`) to indicate strings.

After you done the steps, the whole thing must look like this:

<p align="center">
<img src="docs/hello-world.png" alt= “” width="400" >
</p>

Then go to Shortcuts, and run IOS Stack Machine. You will get a prompt asking which file to run. If you don't see your note in the list, please check your note to see if the title has `.ism` in the end.

## Manipulate the Stack: `push` & `pop`

ISM is a stack machine, meaning it operates using an internal stack. To manipulate this stack in the most basic sense, you can use these two operations:

- `push`

  Adds a constant to the top of the stack.
  
  e.g.
     ```
       push 10      // Stack: top ->      10|
       push 4       // Stack: top ->    4 10|
       push 2       // Stack: top ->  2 4 10|
     ```
- `pop`

  Removes the item on top of the stack. Currently, the value gets lost. (This behaviour may change in the future: the popped value may be put in register A)
  
  e.g
  ```
     push 10      // Stack: top ->      10|
     push 4       // Stack: top ->    4 10|
     pop          // Stack: top ->      10|
     pop          // Stack: top ->        |
  ```

## I/O Instructions: `println` & `readln`

To print a message, you can do `println ISM Rocks!`. However, if you like to see the top of the stack, you can call `println` without any arguments. It may be useful for debugging.

`readln` allows you to take input from the user. It pushes the input to the stack. You can also use with an argument, such as `readln Give me a number`, to change the prompt message. 

## Binary Instructions: `add`, `sub`, `div`, `mul` & `eq`

Binary operations pop 2 items from the top of the stack, and then push the result back. For example, `add` operation in the below program pops 1 and 2, pushes 3 back to the stack:

```
push 1
push 2
add
println
```
This program outputs 3. You can also use `sub`, `div` and `mul` the same way.

Above we used `println` without any arguments. This way of using `println` allows you to see what is the top element of the stack.

One other binary operation is `eq`, which checks if 2 items are equal. For example:

```
push 9
push 8
eq
println       // prints 0
```

```
push 42
push 42
eq
println       // prints 1
```
If two elements are equal, eq returns 1 and 0 otherwise.

## Branching: `jump`, `jnz` & `jpop`

ISM doesn't have for & while loops and if-else statements. It only allows jumping, which anyone can use to implement those higher level expressions. 

- `jump` instruction
    Jumps execution to the provided line. Can be used to skip some part of the code:
    
    ```
    notename.ism
    jump 3
    println This won't we printed unless some other jump will lead here.
    println Hello from line 3!
    ```
- `jnz`instruction
    Jumps execution to the provided line **if** the top of the stack is **not zero**.
    This instruction can be used to implement branching in your code.
    
    ```
    gimmeanumber.ism
    readln Give me a number. (It is better be 10 or I am angry!)
    push 10
    eq
    jnz 7
    println You made me angry!!!
    jump 8
    println Thank you for listening to me! I am happy as ever!
    ```
    
- `jpop` instruction
    Pops a number from the stack, and then jumps to the line with this number. Does not take any arguments.
    
    
## Memory: `load`and `store`

You can assign variables with `store` instruction.

- `store`
  Pops from the stack, and writes to memory.

```
push 3
store x // x is now 3
```

- `load`
  Gets the value of the specified variable, and pushes to the stack.
 
 ```
 push 4
 push 1
 add
 store x
 load x
 println // prints 5
```

## Example: Fibonacci

```
fibbonaci.ism
println This program prints a fibbonaci number.
push 4
push 1
push 2

load A
load B

copy
store A

add
store B

push -1
add
copy
jnz 5
load B
println
```

## Misc.

All functionality of Shortcuts can be added to ISM. However currently, the instruction set is pretty small. One misc. instruction ISM has is `open`. You can use this instruction to open an application in your device. 

e.g. 
```
open Spotify // or
open App Store
```

## Limitations

- Since it is implemented in Shortcuts, ISM runs very slow. This was something I already expected before I start the project.
- There are no `break` functionality in Shortcuts, so I had a little problem while working on `jump` operation. To overcome this I defined a constant value of `999999999999`, which is a really large number. No ISM program can have more lines than this constant (lines that are re-executed after a jump also count in this sum.)

## Contribution

Any contribution is appreciated. But beware that since Shortcuts file format is binary, version control will probably be like hell.
