---
layout: default
title: Assembler&#58; Common errors
description: Understanding what causes common errors and how to fix them
---

# Preface: Using an example

Lets take a look at a basic method. First as source code, then with the assembler.

```java
public static void main(String[] args) {
    String line;
    Scanner scanner = new Scanner(System.in);
    while ((line = scanner.nextLine()).length() > 0) {
        System.out.println("COMPUTED: " + Calculator.evaluate(line));
    }
}
```

We have two variables here. The main method’s arguments `array` is unused. Then we have `nextLine` which is simply set to whatever the  user types in. Each time the user inputs a non-empty string we evaluate  the text in `nextLine` then print it out with the prefix `"COMPUTED: "`. Simple enough, now lets take a look at it in the assembler. I’ve added  some comments to better illustrate what portions of the bytecode relate  to parts of the source code.

```java
DEFINE PUBLIC STATIC main([Ljava/lang/String; args)V
// Scanner scanner = new Scanner(System.in)
A:
NEW java/util/Scanner
DUP
GETSTATIC java/lang/System.in Ljava/io/InputStream;
INVOKESPECIAL java/util/Scanner.<init>(Ljava/io/InputStream;)V
ASTORE scanner
// line = scanner.nextLine()
B:
ALOAD scanner
INVOKEVIRTUAL java/util/Scanner.nextLine()Ljava/lang/String;
DUP
ASTORE line
// (line).length() > 0    (break loop if line <= 0)
C:
INVOKEVIRTUAL java/lang/String.length()I
IFLE E
// System.out.println("COMPUTED: " + Calculator.evaluate(line))
D:
GETSTATIC java/lang/System.out Ljava/io/PrintStream;
NEW java/lang/StringBuilder
DUP
INVOKESPECIAL java/lang/StringBuilder.<init>()V
LDC "COMPUTED: "
INVOKEVIRTUAL java/lang/StringBuilder.append(Ljava/lang/String;)Ljava/lang/StringBuilder;
ALOAD line
INVOKESTATIC calc/Calculator.evaluate(Ljava/lang/String;)D
INVOKEVIRTUAL java/lang/StringBuilder.append(D)Ljava/lang/StringBuilder;
INVOKEVIRTUAL java/lang/StringBuilder.toString()Ljava/lang/String;
INVOKEVIRTUAL java/io/PrintStream.println(Ljava/lang/String;)V
GOTO B
E:
RETURN
```

Perfectly valid bytecode here. Now Lets introduce different errors and see what messages we get back.

# Not a real opcode: NameHere

There is a typo in the instruction opcode.

# Cannot pop operand off an empty stack

Here is a modification to the above code around label `C` that removes the calling context from the call to `line.length()`

This will result in an attempt to pop the calling context off the stack, which is empty, causing the error.

```java
C:
// String is on the stack
POP
// The String has been removed frrom the stack, so now the stack is empty
// ERROR ON THIS LINE:
INVOKEVIRTUAL java/lang/String.length()I
IFLE E
```

Alternatively instead of inserting a `POP` we could have some code that is skipped over by a jump instruction. If a jump skips over some section that sets a variable and you change the label destination that section may no longer be skipped. This may have unintended side effects on the stack such as not having the expected value onthe top at the point of the error.

# Copying an uninitialized value should not occur

This can occur in a few cases. The first case is if you make a typo when specifying some variable. For example, here is a modification to the above code that introduces a typo when using the variable `line`. Instead it will be referenced as `loon`. This is a more tricky case to detect at times since:

- Finding typos is hard because you never intend to spell things wrong in the first place.
- Depending on where the typo is, the error _may not show up_ but instead the logic will not represent what you intended to write.

This will result in an attempt to resolve two separate variables since they do not share the same name, causing the error.

```java
B:
ALOAD scanner
INVOKEVIRTUAL java/util/Scanner.nextLine()Ljava/lang/String;
DUP
// Here the variable is refered to as "line"
ASTORE line
C:
INVOKEVIRTUAL java/lang/String.length()I
IFLE E
D:
GETSTATIC java/lang/System.out Ljava/io/PrintStream;
NEW java/lang/StringBuilder
DUP
INVOKESPECIAL java/lang/StringBuilder.<init>()V
LDC "COMPUTED: "
INVOKEVIRTUAL java/lang/StringBuilder.append(Ljava/lang/String;)Ljava/lang/StringBuilder;
// Here the variable is refered to as "loon" which has never been specified before
// Since the variable has never had its value set, this code is illegal
// (NULL is not a default for object-type variables, but 0 is for primitives)
ALOAD loon
// ERROR ON THIS LINE:
INVOKESTATIC calc/Calculator.evaluate(Ljava/lang/String;)D
INVOKEVIRTUAL java/lang/StringBuilder.append(D)Ljava/lang/StringBuilder;
INVOKEVIRTUAL java/lang/StringBuilder.toString()Ljava/lang/String;
INVOKEVIRTUAL java/io/PrintStream.println(Ljava/lang/String;)V
GOTO B
E:
RETURN
```
The solution here is to double check for typos.

The other situation could be if you have some jump instruction and you modify the destintion label to some other location that does not initialize the variable.


# Cannot call method on null reference

Here is a modification to the above code that replaces the instantiation of the `java/util/Scanner` with a single `null`.

This will cause the method call on the scanner object to call on a provable `null` value, causing the error.

```java
A:
ACONST_NULL
ASTORE scanner
// This will effectively translate to:
// null.nextLine()
B:
ALOAD scanner
// ERROR ON THIS LINE:
INVOKEVIRTUAL java/util/Scanner.nextLine()Ljava/lang/String;
```

The solution here is to make sure you track where `null` is pushed onto the stack via `ACONST_NULL`.

# Argument type was "Apple" expected "Orange"

Here is a modification to the above code that replaces `java/util/Scanner` with `example/ExtendedScanner`. In our example let us assume that `example/ExtendedScanner` is a class that extends `java/util/Scanner`. Let us also assume that **we do not have `example/ExtendedScanner` loaded into Recaf in any of the workspace's resources**.

This will result in an attempt to resolve the type hierarchy between `java/util/Scanner` and `example/ExtendedScanner`. Since we do not have` example/ExtendedScanner` loaded into Recaf, we are unable to prove that it extends `java/util/Scanner`. Thus the assembler will default to assuming the class extends `java/lang/Object`. Calling any non-object method will result in a type conflict, causing the error.

```java
A:
NEW example/ExtendedScanner
DUP
GETSTATIC java/lang/System.in Ljava/io/InputStream;
INVOKESPECIAL example/ExtendedScanner.<init>(Ljava/io/InputStream;)V
ASTORE scanner
// ExtendedScanner extends Scanner... We as people know this, but Recaf does not.
B:
ALOAD scanner
// ERROR ON THIS LINE:
INVOKEVIRTUAL java/util/Scanner.nextLine()Ljava/lang/String;
```

The solution here is to add the code that contains `example/ExtendedScanner` to the workspace.

If we do not have access to the code that contains the class, we can enable _"Generate missing classes"_ in the config window under the _"Assembler"_ tab. 

# Method owner does not match type on stack /  Expected type: Something

The usage of some type indicates it should be the given type shown in the error, but whatever was present on the stack was a different type. This can happen in a couple of situations:

1. Accidentally loading the wrong variable of a different type
2. Accidentally specifying the wrong return type of a method
3. Forgetting to cast some value to the expected type

The solution will vary depending on the situation. Double check your work to look for mistakes.