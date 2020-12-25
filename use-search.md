---
layout: default
title: Search
description: Seach for string constants, field and method references, and more
---

# Searching

In Recaf under the _"Search"_ menu item there are multiple kinds of searches. Each type of search is described below. All search kinds share common behavior:

1. Search input fields that are left empty are counted as _"wildcard"_ search parameters. This means that they will match _any value_. Some examples of using wildcard searches will be outlined below as examples.
2. The match mode for text content can be changed. The supported modes are:
    - **Contains**: If the target text contains the input field text, match.
    - **Equals**:  If the target text is an exact copy of the input field text from start to end, match.
    - **Starts with**: If the target text starts with the text of the input field, match.
    - **Ends with**: If the target text ends with the text of the input field, match.
    - **Regex**: If the target text matches the regular expression pattern of the input field, match. 
3. Searches can be sped up if you choose to skip packages you are not interested in looking at in larger files

# Search Modes

## Strings

![search - strings](img/search-string.png?center)

Finds defined string constants.

### Examples

| Description                                                  | String                            | Match Mode |
| ------------------------------------------------------------ | --------------------------------- | ---------- |
| Match URL strings like `www.example.com` or `http://example.com` | `(www|http(s)?:|ftp:)+[^\s]+[\w]` | Regex      |
| Match common IPv4 address like `192.168.0.1`                 | `(\d{1,3}\.){3}\d{1,3}`           | Regex      |

## Values

![search - strings](img/search-value.png?center)

Finds defined numeric constants. The matched value type is determined by the suffix _(or lack of suffix)_ of the value input text

- `F` will search for `float` values
- `D` will search for `double` values
- `L` will search for `long` values
- No suffix will search for `int` values

Accepted number formats are decimal numbers, floating point numbers, and hexadecimal numbers.

### Examples

| Description                                                  | Value                       |
| ------------------------------------------------------------ | --------------------------- |
| Search for `HKEY_CURRENT_USER` / `HKEY_LOCAL_MACHINE` _([Windows registry](https://stackoverflow.com/questions/62289/read-write-to-windows-registry-using-java))_ | `0x80000001` / `0x80000002` |

## Class references

![search - class](img/search-class.png?center)

Finds where types are referenced. This is not to be confused with member reference. This finds instantiations of the type in the following cases:

- `Example.class`
- `new Example` 
- `x instanceof Example`
- `Example myLocalVariable`

## Member references

![search - references](img/search-member-reference.png?center)

Finds where members are referenced. 

### Examples

| Description                                                  | Owner                 | Name        | Descriptor | Match Mode  |
| ------------------------------------------------------------ | --------------------- | ----------- | ---------- | ----------- |
| Search for all references to anything in the `com/example` package | `com/example`         |             |            | Starts with |
| Search for all references of any member of the class `com/example/Example` | `com/example/Example` |             |            | Equals      |
| Search for all references to any member named `myExample`    |                       | `myExample` |            | Equals      |
| Search for all references to any `int` field                 |                       |             | `I`        | Equals      |
| Search for all references to any method that returns an `int` |                       |             | `)I`       | Ends with   |

*Wildcard searches are very flexible in this search category*

## Member declarations

![search - declarations](img/search-member-declaration.png?center)

Finds field and method definitions.

### Examples

| Description                                                  | Owner   | Name          | Descriptor | Match Mode |
| ------------------------------------------------------------ | ------- | ------------- | ---------- | ---------- |
| Search for all declared fields and methods of any class containing the text `Block` | `Block` |               |            | Contains   |
| Search for all declared fields and methods named named `isActivated` |         | `isActivated` |            | Equals     |
| Search for all declared `int` fields                         |         |               | `I`        | Equals     |
| Search for all declared methods that returns an `int`        |         |               | `)I`       | Ends with  |

## Instructions

### ![search - instructions](img/search-instructions.png?center)

Finds instruction patterns based on disassembled methods.

### Examples

| Description                                                  | Text lines                            | Match Mode  |
| ------------------------------------------------------------ | ------------------------------------- | ----------- |
| Search for all constructor calls by matching the `new Example()` pattern | `NEW`<br />`DUP`<br />`INVOKESPECIAL` | Starts with |
