---
layout: default
title: Config
description: Settings for the UI, key-bindings, decompiler, assembler, and updater
---

# Summary

Recaf's application settings can be changed by clicking the _"Config"_ item in the main menu. There are multiple categories of config values.  Each category contains one or more values that are displayed as a name,  description, and value. 

<center><video controls><source src="img/config-tabs.mp4" type="video/mp4"></video></center>

# Where is config stored?

Config values, along with other related files for Recaf, are stored in different locations depending on your operating system.

- Windows: `%APPDATA%/Recaf`
- Mac: `$HOME/Library/Preferences/Recaf`
- Linux: 
  - `$XDG_CONFIG_HOME/Recaf`
  - `$HOME/.config/Recaf` if `$XDG_CONFIG_HOME` is not set

If you are unsure where the location is set to, you can view it in the _"System information"_ window under the _"Help"_ menu.

![settings location](img/config-location.png?center)