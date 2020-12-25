---
layout: default
title: Themes
description: Customizing how Recaf looks
---

Recaf comes with 2 themes; a flat dark style and the default JavaFx modena style. Each theme is split into two parts:

- **Window**: Standard JavaFX style
- **Text**: Style specific to code-editing

## Adding custom themes

To add your own themes navigate to the Recaf config directory *(See: [Config](https://www.coley.software/Recaf/doc-intro-config.html))*. In this directory are there is a *"style"* sub-directory. In the style directory you can add window and text styles by creating `ui-THEME_NAME.css` and `text-THEME_NAME.css` respectively. You may want to copy an existing theme from the Recaf source code as a basis to work off of.

## Using the theme editor

The theme editor is a heavy work-in-progress. To open it, install the theme plugin *(See: [Plugins](adv-plugins.md))* then launch Recaf. Under the plugins menu you will find a menu item for the theme editor, which will open the editor window. When working in  this editor the theme file `ui-custom.css` is written to  after each modification. Additionally, the UI styles are reloaded after  modifications so that it can be reloaded dynamically. To see the changes live, make sure you set the window theme to *"Custom"*.

You can find the official [JavaFX CSS reference guide here](https://docs.oracle.com/javase/8/javafx/api/javafx/scene/doc-files/cssref.html).