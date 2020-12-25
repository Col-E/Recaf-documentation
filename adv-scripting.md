---
layout: default
title: Scripting
description: Using Recaf as an automated tool
---

Recaf can be used as a command line application. Running it with the argument `--cli` will enable an interactive mode. Here is a demonstration:

<center><video controls><source src="img/cli-demo.mp4" type="video/mp4"></video></center>

Using the `help` command will show the current list of all commands. Each should have automatic tab completion for all arguments  of known data-types.

In order to *"script"* in Recaf, you can write these commands line-by-line to a text file, then run Recaf with the command line argument `--script <file>`. This will execute each line of the file then terminate the program.  Here is an outline of how to use command scripting to process a jar file with some mappings file:

```java
loadworkspace <file-name>
remap <mapping-type> <other-options> <mapping-file>
export <output-file>
```

And here it is filled in with an example:

```java
loadworkspace 20w21a.jar
remap PROGUARD client.txt
export 20w21a-clean.jar
```

It is worth mentioning that the plugin api allows users to register their own custom commands. This  allows you to create your own commands using any utility available in the Recaf source code. 