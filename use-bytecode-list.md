---
layout: default
title: Bytecode format list
description: A guide on Recaf's simplified bytecode format for the assembler
---

{::comment}
Force all tables on the page to render with 100% width
{:/comment}
<style type="text/css" rel="stylesheet">
table { width: 100%; }
</style>

#  Preface

This is a listing of the [Java bytecode instructions](https://en.wikipedia.org/wiki/Java_bytecode_instruction_listings) ordered by the underlying bytecode library *([ASM](https://asm.ow2.io/))* grouping. For instance, `ifeq` and `goto` belong to the `Jump` group. Most of the groupings should make sense and seeing one or two of the instructions should key you into which other ones are also in the  group. What differs this list from the [official instruction specification ](https://docs.oracle.com/javase/specs/jvms/se12/html/jvms-6.html) is that the descriptions have been modified to fit how Recaf represents them.

# Table of Contents

- [Insn](#insn)
- [Integer](#integer)
- [Variable](#variable)
- [Type](#type)
- [Field](#field)
- [Method](#method)
- [InvokeDynamic](#invokedynamic)
- [Jump](#jump)
- [Ldc](#ldc)
- [Increment](#increment)
- [MultiANewArray](#multianewarray)
- [Switch](#switch)
- [Label](#label)
- [Line](#line)

# Insn

| Opcode         | Stack: [before]→[after]                                                                   | Description                                                                                                |
|----------------|-------------------------------------------------------------------------------------------|------------------------------------------------------------------------------------------------------------|
| `aconst_null`  | → `null`                                                                                  | push a `null` reference onto the stack                                                                     |
| `dconst_0`     | → `0.0`                                                                                   | push the constant `0.0` onto the stack                                                                     |
| `dconst_1`     | → `1.0`                                                                                   | push the constant `1.0` onto the stack                                                                     |
| `fconst_0`     | → `0.0f`                                                                                  | push `0.0f` on the stack                                                                                   |
| `fconst_1`     | → `1.0f`                                                                                  | push `1.0f` on the stack                                                                                   |
| `fconst_2`     | → `2.0f`                                                                                  | push `2.0f` on the stack                                                                                   |
| `iconst_m1`    | → `-1`                                                                                    | load the `int` value `−1` onto the stack                                                                   |
| `iconst_0`     | → `0`                                                                                     | load the `int` value `0` onto the stack                                                                    |
| `iconst_1`     | → `1`                                                                                     | load the `int` value `1` onto the stack                                                                    |
| `iconst_2`     | → `2`                                                                                     | load the `int` value `2` onto the stack                                                                    |
| `iconst_3`     | → `3`                                                                                     | load the `int` value `3` onto the stack                                                                    |
| `iconst_4`     | → `4`                                                                                     | load the `int` value `4` onto the stack                                                                    |
| `iconst_5`     | → `5`                                                                                     | load the `int` value `5` onto the stack                                                                    |
| `lconst_0`     | → `0L`                                                                                    | push `long` `0L` onto the stack                                                                            |
| `lconst_1`     | → `1L`                                                                                    | push `long` `1L` onto the stack                                                                            |
| `arraylength`  | arrayref → length                                                                         | get the length of an array                                                                                 |
| `aaload`       | arrayref, index → value                                                                   | load onto the stack a reference from an array                                                              |
| `aastore`      | arrayref, index, value →                                                                  | store into a reference in an array                                                                         |
| `baload`       | arrayref, index → value                                                                   | load a `byte` or Boolean value from an array                                                               |
| `bastore`      | arrayref, index, value →                                                                  | store a `byte` or Boolean value into an array                                                              |
| `caload`       | arrayref, index → value                                                                   | load a `char` from an array                                                                                |
| `castore`      | arrayref, index, value →                                                                  | store a `char` into an array                                                                               |
| `daload`       | arrayref, index → value                                                                   | load a `double` from an array                                                                              |
| `dastore`      | arrayref, index, value →                                                                  | store a `double` into an array                                                                             |
| `faload`       | arrayref, index → value                                                                   | load a `float` from an array                                                                               |
| `fastore`      | arrayref, index, value →                                                                  | store a `float` in an array                                                                                |
| `iaload`       | arrayref, index → value                                                                   | load an `int` from an array                                                                                |
| `iastore`      | arrayref, index, value →                                                                  | store an `int` into an array                                                                               |
| `laload`       | arrayref, index → value                                                                   | load a `long` from an array                                                                                |
| `lastore`      | arrayref, index, value →                                                                  | store a `long` to an array                                                                                 |
| `saload`       | arrayref, index → value                                                                   | load `short` from array                                                                                    |
| `sastore`      | arrayref, index, value →                                                                  | store `short` to array                                                                                     |
| `d2f`          | value → result                                                                            | convert:  `double` to `float`                                                                              |
| `d2i`          | value → result                                                                            | convert:  `double` to `int`                                                                                |
| `d2l`          | value → result                                                                            | convert:  `double` to `long`                                                                               |
| `f2d`          | value → result                                                                            | convert:  `float` to `double`                                                                              |
| `f2i`          | value → result                                                                            | convert:  `float` to `int`                                                                                 |
| `f2l`          | value → result                                                                            | convert:  `float` to `long`                                                                                |
| `i2b`          | value → result                                                                            | convert:  `int` to `byte`                                                                                  |
| `i2c`          | value → result                                                                            | convert:  `int` to `char`                                                                                  |
| `i2d`          | value → result                                                                            | convert:  `int` to `double`                                                                                |
| `i2f`          | value → result                                                                            | convert:  `int` to `float`                                                                                 |
| `i2l`          | value → result                                                                            | convert:  `int` to `long`                                                                                  |
| `i2s`          | value → result                                                                            | convert:  `int` to `short`                                                                                 |
| `l2d`          | value → result                                                                            | convert:  `long` to `double`                                                                               |
| `l2f`          | value → result                                                                            | convert:  `long` to `float`                                                                                |
| `l2i`          | value → result                                                                            | convert:  `long` to `int`                                                                                  |
| `areturn`      | objectref → [empty]                                                                       | return a reference from a method                                                                           |
| `dreturn`      | value → [empty]                                                                           | return a `double` from a method                                                                            |
| `freturn`      | value → [empty]                                                                           | return a `float`                                                                                           |
| `ireturn`      | value → [empty]                                                                           | return an `int` from a method                                                                              |
| `lreturn`      | value → [empty]                                                                           | return a `long` value                                                                                      |
| `return`       | → [empty]                                                                                 | return void from method                                                                                    |
| `dadd`         | value1, value2 → result                                                                   | add two `double` values `value2 + value1`                                                                  |
| `ddiv`         | value1, value2 → result                                                                   | divide two `double` values `value2 / value1`                                                               |
| `dmul`         | value1, value2 → result                                                                   | multiply two `double` values `value2 * value1`                                                             |
| `drem`         | value1, value2 → result                                                                   | get the remainder from a division between two `double` values `(value2 - ((value1 / value2) * value2))`    |
| `dsub`         | value1, value2 → result                                                                   | subtract a `double` from another `value2 - value1`                                                         |
| `fadd`         | value1, value2 → result                                                                   | add two `float` values `value2 + value1`                                                                   |
| `fdiv`         | value1, value2 → result                                                                   | divide two `float` values `value2 / value1`                                                                |
| `fmul`         | value1, value2 → result                                                                   | multiply two `float` values `value2 * value1`                                                              |
| `frem`         | value1, value2 → result                                                                   | get the remainder from a division between two `float` values `(value2 - ((value1 / value2) * value2))`     |
| `fsub`         | value1, value2 → result                                                                   | subtract two `float` values `value2 - value1`                                                              |
| `iadd`         | value1, value2 → result                                                                   | add two `int` values `value2 + value1`                                                                     |
| `idiv`         | value1, value2 → result                                                                   | divide two `int` values `value2 / value1`                                                                  |
| `imul`         | value1, value2 → result                                                                   | multiply two `int` values `value2 * value1`                                                                |
| `irem`         | value1, value2 → result                                                                   | logical `int` remainder `(value2 - ((value1 / value2) * value2))`                                          |
| `isub`         | value1, value2 → result                                                                   | `int` subtract `value2 - value1`                                                                           |
| `iand`         | value1, value2 → result                                                                   | perform a bitwise AND on two `int` values `value2 & value1`                                                |
| `ior`          | value1, value2 → result                                                                   | bitwise `int` OR `value2 | value1`                                                                         |
| `ixor`         | value1, value2 → result                                                                   | `int` xor `value2 ^ value1`                                                                                |
| `ishl`         | value1, value2 → result                                                                   | `int` shift left `value2 << value1`                                                                        |
| `ishr`         | value1, value2 → result                                                                   | `int` arithmetic shift right `value2 >> value1`                                                            |
| `iushr`        | value1, value2 → result                                                                   | `int` logical shift right `value2 >>> value1`                                                              |
| `ladd`         | value1, value2 → result                                                                   | add two `long` values `value2 + value1`                                                                    |
| `ldiv`         | value1, value2 → result                                                                   | divide two `long` values `value2 / value1`                                                                 |
| `lmul`         | value1, value2 → result                                                                   | multiply two `long` values `value2 * value1`                                                               |
| `lrem`         | value1, value2 → result                                                                   | remainder of division of two `long` values `(value2 - ((value1 / value2) * value2))`                       |
| `lsub`         | value1, value2 → result                                                                   | subtract two `long` values `value2 - value1`                                                               |
| `lshl`         | value1, value2 → result                                                                   | bitwise shift left of a `long` value1 by `int` `value2` positions `value2 << value1`                       |
| `lshr`         | value1, value2 → result                                                                   | bitwise shift right of a `long` value1 by `int` `value2` positions `value2 >> value1`                      |
| `lushr`        | value1, value2 → result                                                                   | bitwise shift right of a `long` value1 by `int` `value2` positions, unsigned `value2 >>> value1`           |
| `land`         | value1, value2 → result                                                                   | bitwise AND of two `long` values `value2 ^ value1`                                                         |
| `lor`          | value1, value2 → result                                                                   | bitwise OR of two `long` values `value2 | value1`                                                          |
| `lxor`         | value1, value2 → result                                                                   | bitwise XOR of two `long` values `value2 ^ value1`                                                         |
| `dneg`         | value → result                                                                            | negate a `double` `-value`                                                                                 |
| `fneg`         | value → result                                                                            | negate a `float` `-value`                                                                                  |
| `ineg`         | value → result                                                                            | negate `int` `-value`                                                                                      |
| `lneg`         | value → result                                                                            | negate a `long` `-value`                                                                                   |
| `dcmpg`        | value1, value2 → result                                                                   | compare two `double` values {::nomarkdown}<table><tbody><tr><th>Comparison</th><th>Value</th></tr><tr><td>value1==NaN or<br>value2==NaN</td><td>1</td></tr><tr><td>value1 &gt; value2</td><td>1</td></tr><tr><td>value1==value2</td><td>0</td></tr><tr><td>value1 &lt; value2</td><td>-1</td></tr></tbody></table>{:/}   |
| `dcmpl`        | value1, value2 → result                                                                   | compare two `double` values {::nomarkdown}<table><tbody><tr><th>Comparison</th><th>Value</th></tr><tr><td>value1==NaN or<br>value2==NaN</td><td>-1</td></tr><tr><td>value1 &gt; value2</td><td>1</td></tr><tr><td>value1==value2</td><td>0</td></tr><tr><td>value1 &lt; value2</td><td>-1</td></tr></tbody></table>{:/}  |
| `fcmpg`        | value1, value2 → result                                                                   | compare two `float` values  {::nomarkdown}<table><tbody><tr><th>Comparison</th><th>Value</th></tr><tr><td>value1==NaN or<br>value2==NaN</td><td>1</td></tr><tr><td>value1 &gt; value2</td><td>1</td></tr><tr><td>value1==value2</td><td>0</td></tr><tr><td>value1 &lt; value2</td><td>-1</td></tr></tbody></table>{:/}   |
| `fcmpl`        | value1, value2 → result                                                                   | compare two `float` values  {::nomarkdown}<table ><tbody><tr><th>Comparison</th><th>Value</th></tr><tr><td>value1==NaN or<br>value2==NaN</td><td>-1</td></tr><tr><td>value1 &gt; value2</td><td>1</td></tr><tr><td>value1==value2</td><td>0</td></tr><tr><td>value1 &lt; value2</td><td>-1</td></tr></tbody></table>{:/} |
| `lcmp`         | value1, value2 → result                                                                   | compare two `long` values   {::nomarkdown}<table><tr><th>Comparison</th><th>Value</th></tr><tr><td>value1==value2</td><td>0</td></tr><tr><td>value1 &gt; value2</td><td>1</td></tr><tr><td>else</td><td>-1</td></tr></table>{:/} |
| `athrow`       | objectref → [empty], objectref                                                            | throws an error or exception _(notice that the rest of the stack is cleared, leaving only a reference to the `Throwable`)_                                                                                 |
| `dup`          | value → value, value                                                                      | duplicate the value on top of the stack                                                                                                                                                                    |
| `dup_x1`       | value2, value1 → value1, value2, value1                                                   | insert a copy of the top value into the stack two values from the top. `value1` and `value2` must not be of the type `double` or `long`.                                                                   |
| `dup_x2`       | value3, value2, value1 → value1, value3, value2, value1                                   | insert a copy of the top value into the stack two _(if `value2` is `double` or `long` it takes up the entry of `value3`, too)_ or three values (if `value2` is neither `double` nor `long`) from the top   |
| `dup2`         | {value2, value1} → {value2, value1}, {value2, value1}                                     | duplicate top two stack words _(two values, if `value1` is not `double` nor long; a single value, if value1 is `double` or `long`)_     |
| `dup2_x1`      | value3, {value2, value1} → {value2, value1}, value3, {value2, value1}                     | duplicate two words and insert beneath third word _(see explanation above)_                                |
| `dup2_x2`      | {value4, value3}, {value2, value1} → {value2, value1}, {value4, value3}, {value2, value1} | duplicate two words and insert beneath fourth word                                                         |
| `pop`          | value →                                                                                   | discard the top value on the stack                                                                         |
| `pop2`         | {value2, value1} →                                                                        | discard the top two values on the stack _(or one value, if it is a `double` or long)_                      |
| `swap`         | value2, value1 → value1, value2                                                           | swaps two top words on the stack _(note that `value1` and `value2` must not be `double` or long)_          |
| `monitorenter` | objectref →                                                                               | enter monitor for object _("grab the lock" – start of synchronized() section)_                             |
| `monitorexit`  | objectref →                                                                               | exit monitor for object _("release the lock" – end of synchronized() section)_                             |
| `nop`          | [No change]                                                                               | do nothing                                                                                                 |

# Integer

| Opcode              | Stack: [before]→[after] | Description                                                                                                |
|---------------------|-------------------------|------------------------------------------------------------------------------------------------------------|
| `bipush` {::nomarkdown}<ul><li>value</li></ul>{:/}        | → value                 | push a `byte` onto the stack as an `int` value                         |
| `sipush` {::nomarkdown}<ul><li>value</li></ul>{:/}        | → value                 | push a `short` onto the stack as an `int` value                        |
| `newarray` {::nomarkdown}<ul><li>descriptor</li></ul>{:/} | count → arrayref        | create new array with count elements of primitive type identified by descriptor {::nomarkdown}<table ><tr><th>Type</th> <th>Descriptor alias</th></tr><tr><td>boolean</td><td>Z</td></tr><tr><td>char</td><td>C</td></tr><tr><td>float</td><td>F</td></tr><tr><td>double</td><td>D</td></tr><tr><td>byte</td><td>B</td></tr><tr><td>short</td><td>S</td></tr><tr><td>int</td><td>I</td></tr><tr><td>long</td><td>J</td></tr></table>{:/} |

# Variable

| Opcode       | Stack: [before]→[after] | Description                                                 |
|--------------|-------------------------|-------------------------------------------------------------|
| `iload` {::nomarkdown}<ul><li>value</li></ul>{:/}  | → value                 | load an `int` value from a local variable index               |
| `lload` {::nomarkdown}<ul><li>value</li></ul>{:/}  | → value                 | load a `long` value from a local variable index               |
| `fload` {::nomarkdown}<ul><li>value</li></ul>{:/}  | → value                 | load a `float` value from a local variable index              |
| `dload` {::nomarkdown}<ul><li>value</li></ul>{:/}  | → value                 | load a `double` value from a local variable index             |
| `aload` {::nomarkdown}<ul><li>value</li></ul>{:/}  | → objectref             | load a reference onto the stack from a local variable index   |
| `istore` {::nomarkdown}<ul><li>value</li></ul>{:/} | value →                 | store `int` value into variable index                         |
| `lstore` {::nomarkdown}<ul><li>value</li></ul>{:/} | value →                 | store a `long` value in a local variable index                |
| `fstore` {::nomarkdown}<ul><li>value</li></ul>{:/} | value →                 | store a `float` value into a local variable index             |
| `dstore` {::nomarkdown}<ul><li>value</li></ul>{:/} | value →                 | store a `double` value into a local variable index            |
| `astore` {::nomarkdown}<ul><li>value</li></ul>{:/} | objectref →             | store a reference into a local variable index                 |

# Type

| Opcode          | Stack: [before]→[after] | Description                                                                            |
|-----------------|-------------------------|----------------------------------------------------------------------------------------|
| `new` {::nomarkdown}<ul><li>type</li></ul>{:/}        | → objectref             | create new object of `type`                                                                |
| `anewarray` {::nomarkdown}<ul><li>type</li></ul>{:/}  | count → arrayref        | create a new array of references of length `count` and component `type` identified by type |
| `checkcast` {::nomarkdown}<ul><li>type</li></ul>{:/}  | objectref → objectref   | checks whether an `objectref` is of a certain specified `type`                             |
| `instanceof` {::nomarkdown}<ul><li>type</li></ul>{:/} | objectref → result      | determines if an object `objectref` is of a given `type`                                   |

# Field

| Opcode                  | Stack: [before]→[after] | Description                                                                    |
|-------------------------|-------------------------|--------------------------------------------------------------------------------|
| `getfield` {::nomarkdown}<ul><li>owner</li><li>name</li><li>desc</li></ul>{:/}  | objectref → value       | get an instance field defined by the `owner` class and the field's `name` and `desc` |
| `getstatic` {::nomarkdown}<ul><li>owner</li><li>name</li><li>desc</li></ul>{:/} | → value                 | get a static field defined by the `owner` class and the field's `name` and `desc`    |
| `putfield` {::nomarkdown}<ul><li>owner</li><li>name</li><li>desc</li></ul>{:/}  | objectref, value →      | set an instance field defined by the `owner` class and the field's `name` and `desc` |
| `putstatic` {::nomarkdown}<ul><li>owner</li><li>name</li><li>desc</li></ul>{:/} | value →                 | set a static field defined by the `owner` class and the field's `name` and `desc`    |


# Method

| Opcode                        | Stack: [before]→[after]               | Description                                                                                                                                                |
|-------------------------------|---------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `invokeinterface` {::nomarkdown}<ul><li>owner</li><li>name</li><li>desc</li></ul>{:/} | objectref, [arg1, arg2, ...] → result | invokes an interface method defined by the `owner` class and the method's `name` and `desc` on object `objectre`f and puts the result on the stack _(might be `void`)_ |
| `invokespecial` {::nomarkdown}<ul><li>owner</li><li>name</li><li>desc</li></ul>{:/}   | objectref, [arg1, arg2, ...] → result | invokes an instance method defined by the `owner` class and the method's `name` and `desc` on object `objectref` and puts the result on the stack _(might be `void`)_  |
| `invokestatic` {::nomarkdown}<ul><li>owner</li><li>name</li><li>desc</li></ul>{:/}    | [arg1, arg2, ...] → result            | invokes a static method defined by the `owner` class and the method's `name` and `desc` and puts the result on the stack _(might be `void`)_                           |
| `invokevirtual` {::nomarkdown}<ul><li>owner</li><li>name</li><li>desc</li></ul>{:/}   | objectref, [arg1, arg2, ...] → result | invokes a virtual method defined by the `owner` class and the method's `name` and `desc` on object `objectref` and puts the result on the stack _(might be `void`)_    |

# InvokeDynamic

| Opcode                                                                                                                                                 | Stack: [before]→[after]   | Description                                                                                                           |
|--------------------------------------------------------------------------------------------------------------------------------------------------------|---------------------------|-----------------------------------------------------------------------------------------------------------------------|
| `invokedynamic` {::nomarkdown}<ul><li>definition</li><ul><li>name, desc</li></ul><li>bootstrap handle</li><ul><li>owner, name, desc</li></ul><li>bootstrap arguments[]</li></ul>{:/} | [arg1, arg2 ...] → result | invokes a dynamic method and puts the result on the stack _(might be `void`)_. The `callsite` handles the dynamic invocation. |

# Jump

| Opcode          | Stack: [before]→[after] | Description                                   |
|-----------------|-------------------------|-----------------------------------------------|
| `goto` {::nomarkdown}<ul><li>label</li></ul>{:/}      | [no change]             | jump to `label`                                   |
| `if_acmpeq` {::nomarkdown}<ul><li>label</li></ul>{:/} | value1, value2 →        | if references `value1 == value2`, jump to `label` |
| `if_acmpne` {::nomarkdown}<ul><li>label</li></ul>{:/} | value1, value2 →        | if references `value1 != value2`, jump to `label` |
| `if_icmpeq` {::nomarkdown}<ul><li>label</li></ul>{:/} | value1, value2 →        | if ints `value1 == value2`, jump to `label`       |
| `if_icmpge` {::nomarkdown}<ul><li>label</li></ul>{:/} | value1, value2 →        | if ints `value1 >= value2`, jump to `label`       |
| `if_icmpgt` {::nomarkdown}<ul><li>label</li></ul>{:/} | value1, value2 →        | if ints `value1 > value2`, jump to `label`        |
| `if_icmple` {::nomarkdown}<ul><li>label</li></ul>{:/} | value1, value2 →        | if ints `value1 <= value2`, jump to `label`       |
| `if_icmplt` {::nomarkdown}<ul><li>label</li></ul>{:/} | value1, value2 →        | if ints `value1 < value2`, jump to `label`        |
| `if_icmpne` {::nomarkdown}<ul><li>label</li></ul>{:/} | value1, value2 →        | if ints `value1 != value2`, jump to `label`       |
| `ifeq` {::nomarkdown}<ul><li>label</li></ul>{:/}      | value →                 | if `value == 0`, jump to `label`                  |
| `ifge` {::nomarkdown}<ul><li>label</li></ul>{:/}      | value →                 | if `value >= 0`, jump to `label`                  |
| `ifgt` {::nomarkdown}<ul><li>label</li></ul>{:/}      | value →                 | if `value > 0`, jump to `label`                   |
| `ifle` {::nomarkdown}<ul><li>label</li></ul>{:/}      | value →                 | if `value <= 0`, jump to `label`                  |
| `iflt` {::nomarkdown}<ul><li>label</li></ul>{:/}      | value →                 | if `value < 0`, jump to `label`                   |
| `ifne` {::nomarkdown}<ul><li>label</li></ul>{:/}      | value →                 | if `value != 0`, jump to `label`                  |
| `ifnonnull` {::nomarkdown}<ul><li>label</li></ul>{:/} | value →                 | if `value != null`, jump to `label`               |
| `ifnull` {::nomarkdown}<ul><li>label</li></ul>{:/}    | value →                 | if `value == null`, jump to `label`               |

# Ldc

| Opcode    | Stack: [before]→[after] | Description                                                                 |
|-----------|-------------------------|-----------------------------------------------------------------------------|
| `ldc` {::nomarkdown}<ul><li>value</li></ul>{:/} | → value                 | push a constant value _(`String`, `int`, `float`, `long`, `double`, `Class`, or `Handle`)_ onto the stack |

# Increment

| Opcode           | Stack: [before]→[after] | Description                                             |
|------------------|-------------------------|---------------------------------------------------------|
| `iinc` {::nomarkdown}<ul><li>index</li><li>amount</li></ul>{:/} | [No change]             | increment local variable `index` by a given `amount` _(`byte`)_ |

# MultiANewArray

| Opcode                  | Stack: [before]→[after]         | Description                                                      |
|-------------------------|---------------------------------|------------------------------------------------------------------|
| `multianewarray` {::nomarkdown}<ul><li>desc</li><li>dims</li></ul>{:/} | count1, [count2,...] → arrayref | create a new array of `dims` dimensions of type identified by `desc` |

# Switch

| Opcode       | Stack: [before]→[after] | Description                                                                                                         |
|--------------|-------------------------|---------------------------------------------------------------------------------------------------------------------|
| `lookupswitch` | key →                   | a target address is looked up from a table using a `key` and execution continues from the instruction at that address |
| `tableswitch`  | index →                 | continue execution from an address in the table at offset `index`                                                     |

# Label

| Opcode | Stack: [before]→[after] | Description                                                                                      |
|--------|-------------------------|--------------------------------------------------------------------------------------------------|
| `label`  | [No change]             | marker in bytecode for the beginning of a block of opcodes; referenced by jump and switch instructions. |

# Line

| Opcode     | Stack: [before]→[after] | Description                                                                                    |
|------------|-------------------------|------------------------------------------------------------------------------------------------|
| `line` {::nomarkdown}<ul><li>line</li></ul>{:/} | [No change] | marker for where the next instruction denotes the beginning of a given line in the original source. |
