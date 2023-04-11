# DevEnvironmentDemo

TL;DR: Linux users will really only need a few things to make this NesHacker Dev magic happen

- A version of the cc65 assembler suite either from your official repositories in aptitude, yum, or pacman OR built yourself from the ca65 source code at https://github.com/cc65/cc65.
- A text editor of your choice (the Too Long part below outlines why VSCode on Linux might give you a headache with this task)
- Any NES emulator you're commfortable with (I'm using FCEUX)

- Clone this github repo
- Assemble the project manually with:
```
cl65 --verbose --target nes demo.s -o demo.nes
```
- This should cleanly assmeble the demo.nes file which you can test in your favored NES emulator
---
OK, here's some issues for Linux users following along:

The brokenness of the steps outlined in the NES Development Envirconment video at https://www.youtube.com/watch?v=RtY5FV5TrIU MIGHT come from some issues with the official Microsoft-built version of VSCode for Linux, the recommended ca65 extension, the build task tool contained within, or some combination of all of the above.

- What has to happen first:
Edit line 2 in the "executable" key in cl65config.json NesHacker's repo to reflect the location of your Linux version of the cl65 assembler. If it's in your PATH, you can just feed it the name of the executable, you don't need the absolute path.

- What *should* happen:
Running the "Run Build Tasks" command in VSCode's command palette should make this a clean build.

- What *does* happen (for me):
Running the "Run Build Tasks" command in VSCode's command palette causes a linking error. A demo.o object code file is attempted to be built, but either VSCode, the ca65 extension, the build task, or something wrong in all of the above will not adhere to the params key in the build task.
Instead, VSCode attempts to run cl65 with no parameters against demo.s and the default target for cl65 is the Commodore 64, using that target's cfg file and throwing an error.

- *Where* does this happen (for me):
Happens on Ubuntu 22.04 as well as updated Arch builds

- *Why* does this happen (for me):
I haven't a clue what causes the build task in VSCode for Linux to ignore the params key in the cl65config.json file, but that's where things break down.
