---
layout: default
title: Editing&#58; Making changes with bytecode 
description: Covering all the relevant bits on bytecode editing
---

# Summary

The primary way to edit bytecode is through the assembler. Bytecode is disassembled and simplified to make editing it as easy as possible. You can find the full list of features here: [Assembler](use-assembler.md)

# How do you access the assembler?

When you right click a field or method definition in Recaf selecting _"Edit with assembler"_ will open the assembler window. Fields and methods both use the same assembler system, but each use a different syntax for defining field or method specific properties.

<center><video controls><source src="img/assembler-access.mp4" type="video/mp4"></video></center>

# Making changes

The assembler represents bytecode as text. Each diassembled line represents an instruction or some debug information _(such as line numbers)_. To add your changes, just insert a new line and write your additional instructions. Or to remove things, delete the lines.

If you are unfamiliar with bytecode and only need to insert additional logic you can insert a line with `EXPR <expression>`. For example. `EXPR System.out.println("hello");`. These one-line expressions also support `if` statements. So you can write `EXPR if (myBoolArg) doSomething();`.  If you wish to prematurely exit a method you may want to write something like `EXPR if (myBoolArg) return;`. If the method return type is something other than `void` you would return some additional value.

<center><video controls><source src="img/expression_control_flow.mp4" type="video/mp4"></video></center>

All changes are subject to bytecode verification, so if you make a mistake Recaf will tell you in the bottom panel under the _"Errors"_ tab.  You can click the error in this tab to immediately jump to the affected line. The line the error occured on will also show a red indicator next to it.

For more information see: 

- [Bytecode instructions](use-bytecode-list.md)
- [Assembler](use-assembler.md)
- [Common assembler errors](use-assembler-errors.md)