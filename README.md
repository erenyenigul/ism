<img src="docs/logo.png" alt=“ISM-logo” width="50">

# IOS Stack Machine

## Ever wondered if you can use Apple Notes to write code? 📝
(probably not.)
Well, now you can!

IOS Stack Machine (ISM) is an interpreter implemented in Apple Shortcuts, thus it works in all Apple devices that have Shortcuts app installed.
## Quick Start: Hello World

After installing ISM to your device, go ahead and open Notes app and create a new note. The name of your note should end with `.ism`, so that ISM can see your code. That's why after naming your note, append `.ism`to the end of title.

To the next line, append this code.

```asm
println Hello world!
```
In ISM, every line must contain a single instruction. First word in the line is the instruction name and the rest is the arguments. Beware that number of spaces between each argument, or between argument and the instruction matters. There should be a single space.

Also, as you've also seen, you don't need to use double quotes (`"`) to indicate strings.

After you done the steps, the whole thing must look like this:

<p align="center">
<img src="docs/hello-world.png" alt= “” width="400" >
</p>

Then go to Shortcuts, and run IOS Stack Machine. You will get a prompt asking which file to run. If you don't see your note in the list, please check your note to see if the title has `.ism` in the end.

## Manipulate the Stack: push & pop
