---
layout: default
title: Editing
description: Hub page for editing capabilities
---

# Relevant content

- The different class modes
    - Decompile mode
    - Table mode
    - Hex mode
- [Making changes with bytecode](use-edit-via-bytecode.md)
- [Making changes with decompiled code](use-edit-via-decompile.md)
- History and undo

# The basic steps

1. Load a file to edit, plus any supporting content
2. Navigate to the class you want to edit
3. Make your changes and save them
4. Export the modified file

## Basic step 1: Loading

To load a file you want to edit, load it from the _"File"_ menu and select _"Load"_, or drop it into the Recaf window area that shows the prompt _"Drop application to begin"_.

You can add supporting libraries from the _"File"_ menu with _"Add library"_.

For more information see:

- [Workspaces](use-workspace.md)

## Basic step 2: Find the class you want to edit

To find the class in the workspace, you can open the package folders in the tree display until you find the class. Alternatively, you can type the class's name in the search field to quickly find it.

For more information see: 

- [Workspaces](use-workspace.md)

## Basic step 3: Make your changes

There are two main ways to make changes. Editing the decompiled code as source code, and making bytecode level changes.

### Editing decompiled code

If your input file is not obfuscated and you have configured compiler support, then making your changes to the decompiled code and would be the quickest and easiest approach. This approach will require that you have either all the referenced classes loaded in the workspace or enabled phantom class generation with _"Generate missing classes"_ in the config window. It is worth noting though that this is subject to the accuracy of the decompiled code and may not work in all cases. You can try the different decompilers and see which is the best fit for your situation.

For more information see: 

- [Making changes with bytecode](use-edit-via-bytecode.md)

### Editing bytecode

If your input file is obfuscated _(which typically breaks compiler support due to decompile errors)_ or you cannot use the compiler feature, then you will want to make changes at the bytecode level. Right click on the member you want to edit _(For decompile mode, select its name)_ and choose _"Open with assembler"_. 

The assembler allows you to edit bytecode as text. If your input contains line number debug information you can easily find what bytecode relates to each line of code by looking at the `LINE` statements. The code after each statement is on that line. 

If your change is a simple one-liner you can write it as pure source code with the `EXPR` statement. For example, `EXPR System.out.println(argString);` or `EXPR if (argBool) return true;`

If your change is more complicated then you can write it as standard bytecode.

For more information see: 

- [Making changes with bytecode](use-edit-via-bytecode.md)
- [Bytecode instructions](use-bytecode-list.md)

## Basic step 4: Export the modified file

In the _"File"_ menu select _"Export program"_ and select a file location to save to.

For more information see: 

- [Workspaces](use-workspace.md)
