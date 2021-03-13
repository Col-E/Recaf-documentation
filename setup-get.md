---
layout: default
title: Setup&#58; Getting Recaf
description: Steps on ensuring you can install and run Recaf
---
# Prerequisites

Recaf's only pre-requisite is that you have Java installed. However using older versions of Java may affect feature availability. See the following documentation guides for more information:


- [Java 8](setup-java8.md)
- [Java 11+](setup-java8.md)

If you have Java 9 or 10 installed, please update to Java 11 or higher.

# Installing

Recaf is distributed as an executable jar file. You can get the latest release in the following ways:

1. Visiting the project's [release's section on GitHub](https://github.com/Col-E/Recaf/releases) and downloading the latest `recaf-2.X.X-J8-jar-with-dependencies.jar`
2. Download using [homebrew](https://formulae.brew.sh/cask/recaf) with `brew install --cask recaf`
3. Download from the [Arch user repository](https://aur.archlinux.org/packages/recaf/)
4. Download or clone the project then run the build script: `build/build.sh`

# Updating

Recaf will notify you when a new version has been released. Mousing away from the prompt will hide it, but it will still be accessible under the **Help** menu.

You disable or can change how often Recaf checks for updates in the config window.

![prompt example](img/update-prompt.png?style=center)

# Running with specific Java versions

Recaf will run using the Java version that your system defaults to.  

If you are using Java 8 and you want to use a feature like JVM attaching or recompiling you will need to ensure the default version is a JDK, not a JRE.

You can alternatively specify the version used when launching via command line:

<center><video controls><source src="img/run-version.mp4" type="video/mp4"></video></center> 

----------------------------------

# Troubleshooting

## Double clicking the recaf jar does not open Recaf

**Solution #1**: Make sure you have downloaded the correct jar. Its the one with the long name ending in `J8-jar-with-dependencies.jar`. You can rename the file after downloading.

**Solution #2**: Make sure your operating system associated clicking jar files with running them.
 - Windows: [Make sure your registry entry for the file type association is pointing to the correct Java version, and includes the `-jar` argument](https://superuser.com/questions/1194758/unable-to-run-jar-files-by-double-clicking-them-on-windows-7)
 - Mac: [Use Automator to associate the file extension](https://github.com/AdoptOpenJDK/openjdk-installer/issues/93#issuecomment-633135558)
 - Linux: [Make sure Java is installed and the jar file extension uses the correct Java version](https://askubuntu.com/questions/192914/how-run-a-jar-file-with-a-double-click)
 
 You can valdidate that the issue is the file type association by running the jar in a terminal via `java -jar recaf.jar` _(With the correct Recaf jar)_
 
 If running Recaf with the terminal shows a crash report, [please open a bug report](https://github.com/Col-E/Recaf/issues/new?template=bug_report.md).