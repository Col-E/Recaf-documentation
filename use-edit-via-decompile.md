---
layout: default
title: Editing&#58; Making changes with decompiled code 
description: Covering all the relevant bits on recompiling decompiled code
---

# Summary

The easiest way to edit bytecode is to edit it as decompiled source. This does not work for highly complex cases and obfuscation, but for most simple edits its all you'll ever need to do. Simply open the class, make your changes as plain Java code, and save.

# Requirements

## Configuring compiler support

To edit decompiled code you must make sure that you have enabled compiler support in Recaf by configuring your local Java install. You can read the guides on how to verify this information here:

- [Java 8](setup-java8.md)
- [Java 11+](setup-java8.md)

## Loading compile dependencies as supporting libraries

Because we're just compiling source code we need to make sure all the references in the code can be resolved. This means you must either:

- Add each dependency to the workspace
- Enable phantom class generation via _"Generate missing classes"_ in the config window

In most cases generating missing classes will be much faster and all you'll need to do. When you load a file Recaf will analyze it in the background and generate _"phantom classes"_ for all the discovered references. Once complete the compiler will use these as compile dependencies so you don't have to manually add each library to the workspace.

# Making changes

Once you have the requirements above set up, editing code in decompile mode is as simple as it gets. 

1. Find the class you want to edit
2. Make sure there are no decompiler syntax errors
3. Make your changes as Java code
4. Save _(`Control + S`)_

If the current decompiler emits code that contains errors, try another one. Remember, your changes are not the only thing that may be modified if the decompiler does not properly recreate the source code.

Not all errors are shown immediately. Additional compiler errors will be shown when you first attempt to save after the compiler is invoked.