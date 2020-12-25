---
layout: default
title: Class modes
description: The different ways to represent a class, and when each is best
---

When opening class files in Recaf, you have 3 different display modes. For all modes you can save your changes with `Control + S` *(Binds are modifiable in the config window)*. When the save was a success the edges of the editor window will flash  green. Make sure you see a green flash to verify your changes are saved  before you export your file. For additional information check the  documentation pages of each class mode, listed below.

![save glow](img\save-glow.gif?center)

## Changing the mode

The default mode is set to *Decompile*. There are cases where this is less than optimal. In order to change the class display mode there are two approaches:

**1. Change the config**

To permanently change the mode you can open the config window by selecting *"Config"* on the menu bar. In the display tab change the *"Class mode"* to something else. 

Any new class that is opened will use this new mode. Tabs that are already open are not changed.

**2. Change the tab's config**

To change the mode for only the one class, you can right  click on the tab title and change the mode in addition to changing the  decompiler. 

Any new class that is opened will still use whatever is  specified in the config. This only changes the config for the current  tab.

**Demo**

![changing modes demo](img/changing-modes.gif?center)

# Decompile Mode

The decompile view mode is typically the most effective way to display classes. It works by decompiling the class and using the [JavaParser library](https://github.com/javaparser/javaparser) to analyze the decompiled code. When you right click on some text  JavaParser can figure out what you have selected, be it a class, field,  or method. With this knowledge Recaf will show you a context menu with  relevant options. For field and method definitions this will allow you  to bring up the assembler window for the selected field or method. If  you select a reference to a field or method and not the definition  itself then the option to jump to its definition will be presented  instead.

![decompile mode](img/mode-decompile.png?center)

This view mode is designed to be the most easy to use and familiar of the options since it presents the class in a familiar source-like  fashion. Additionally this mode will allow you to compile the decompiled code if the code is compliant with the installed Java compiler on your  system. If no Java compiler is found you will not be able to recompile  code this way, but the assembler will always be there for you. Please be aware that this is a direct call to javac so  any compile errors you have that show up when you attempt to save are  compiler errors, not Recaf errors. There are plenty of edge cases that  may cause compiling to fail that are not immediately obvious. Please  double check what you are compiling.

Recaf provides support for the following decompilers:

- [CFR](https://github.com/leibnitz27/cfr)
- [FernFlower](https://github.com/fesh0r/fernflower)
- [Procyon](https://bitbucket.org/mstrobel/procyon/src/default/)

The primary decompiler that will be used in this mode can be  changed in the config window’s decompile tab. Different decompilers  format the code slightly differently and may handle certain classes  better than others. If at first one decompiler fails to fully  reconstruct the code into something that is parseable, try another  decompiler. If you are looking at an obfuscated class then it is likely  that the decompilers will not be able to fully interpret the code. In  this case you should switch to table mode which in the next section.

**Pros**:

- Easy to understand for beginners since everything is laid out in a familiar way.
  - Right click text for context-sensitive menus, allowing access to editing and navigation functions.
- Easy to make changes by recompiling decompiled code.
  - Hit the save keybind *(`Control + S`)* to recompile the decompiled code.
  - Requires all referenced classes to be accessible in the workspace. 

**Cons**:

- Does not handle obfuscated code well. JavaParser does not work if the code isn’t *"valid"*. Thus Recaf will have no way to understand what you are selecting and will not show context menus.

# Table Mode

The table view mode is designed as a foolproof display mode that will always work even in cases where the class is heavily obfuscated. Right  clicking on table rows of both fields and methods behaves like clicking  on the respective definitions in the decompile view mode.

![table mode](img/mode-table.png?center)

**Pros**:

- Works regardless of obfuscation.

**Cons**:

- Not as intuitive as decompile mode since you cannot see the method's logic.

# Hex Mode

The hex mode is a very basic hex editor implementation. This will  allow for precision editing of files. There is no contextual actions  here, its just pure hex editing.

![hex mode](img/mode-hex.png?center)

**Pros**:

- True lossless/precision editing.
  - In other modes, making changes will reorganize the class file's constant pool due to the usage of the [ASM bytecode library](https://asm.ow2.io/javadoc/org/objectweb/asm/ClassWriter.html#COMPUTE_FRAMES).
- Works regardless of obfuscation.

**Cons**:

- Difficult if you are not familiar with hex editors and the [class file format](https://docs.oracle.com/javase/specs/jvms/se14/html/jvms-4.html).
  - You can interactively learn the format by using [Kaitai struct's web IDE](https://ide.kaitai.io/)
    - Select `kaitai.io/formats/executable/java_class.ksy`
    - At the bottom left corner, click the upload button and select a class file to analyze.