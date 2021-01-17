---
layout: default
title: Plugins
description: Adding additional functionality to Recaf
---

# Installing plugins

To install a plugin for Recaf, drop it into the *"plugins"*  directory inside Recaf's settings directory. When you launch Recaf check to see if the plugin has been loaded by looking for it in the plugin  manager *("Plugins > Manage plugins")*. If the plugin is missing, check the log output for errors and contact the plugin author with a bug report.

# Current plugins

| Name             | Description                                                  | Required Recaf version | Last Updated Version | Download                                                     |
| ---------------- | ------------------------------------------------------------ | ---------------------- | -------------------- | ------------------------------------------------------------ |
| String replacer  | Replace text globally *(Exact match)*                        | 2.0.0                  | 1.0.0                | [strrep](plugins/strrep-1.0.0.jar)                           |
| RPC              | A Discord RichPresence plugin for Recaf                      | 2.0.0                  | 1.0.0                | [FlowArg/RecafPluginRPC](https://github.com/FlowArg/RecafPluginRPC) |
| AntiAntiDebug    | Prevents JVMs from detecting Recaf                           | 2.0.0                  | 1.0.0                | [xxDark/AntiAntiDebug](https://github.com/xxDark/AntiAntiDebug) |
| Decompile Export | Adds a decompile-all feature to resources, classes, and packages in the navigation tree | 2.0.0                  | 1.1.0                | [decompile](plugins/decompile-1.1.0.jar)                     |
| Theme Editor     | Make the theme editor available                              | 2.0.0                  | 1.0.0                | [theme](plugins/theme-1.0.0.jar)                             |
| Illegal Renamer  | Renames classes / methods / fields with names that include illegal characters, or match reserved keywords. Allowed characters are: Letters, Digits, `$`, `/` | 2.0.0                  | 1.3.0                | [illegalrenamer](plugins/illegalrenamer-1.3.0.jar)           |

# Developing Plugins

Recaf comes with a plugin system. You can create your own easily by setting up a workspace using this template project: [Recaf-plugin-workspace](https://github.com/Recaf-Plugins/Recaf-plugin-workspace).  The plugin api interfaces are located in `me.coley.recaf.plugin.api` package. Your plugin must implement one of the following interfaces:

**BasePlugin**

- No unique behavior.

**CommandPlugin**

- Allows adding new commands to Recaf’s command-line mode.
- Commands are generated using [picocli](https://picocli.info/) annotations. Simply annotate your class as described on [picocli’s website](https://picocli.info/) and the command will be automatically recognized.

**ConfigurablePlugin**

- Allows plugins to keep persistent config values. Each plugin is granted its own tab in the config window.
  - Annotate config fields with `@Conf(value="Title", noTranslate=true)`
  - Specify the config tab name by implementing getConfigTabTitle()
  - Optional:            
    - Specify custom serialization/deserialization for fields using `supported(Class)`, `loadType(FieldWrapper, Class, JsonValue)`, `saveType(FieldWrapper, Object, JsonObject)`
    - Specify custom UI components for displaying fields using `addFieldEditors(Map)`
      - By default, any `boolean`, `enum`, or `Binding` *(Recaf keybind type)* field will automatically have editor controls specified.

**ContextMenuInjectorPlugin**

- Allows modifying any of the context-menus shown in Recaf.

**EntryLoaderProviderPlugin**

- Allows the usage of custom archive entry handlers.            
  - Entry loaders are fed the raw `byte[]` of all files in an archive.

**ExportInterceptorPlugin**

- Allows the contents of exported files to be modified before being written to the destination.

**KeybindProviderPlugin**

- Allows plugins to specify custom keybinds globally, for class-views, and for file-views.

**LoadInterceptorPlugin**

- Allows the contents of imported files to be modified before being loaded into a Recaf resource.            
  - This is different from the `EntryLoaderProviderPlugin` since there is no per-resource context of loaded items.

**MenuProviderPlugin**

- Allows the plugin to create a custom menu item to be shown under the plugins menu.

**StartupPlugin**

- Allows the plugin to notified when Recaf starts up.            
  - The plugin is also given access to the controller instance.

**WorkspacePlugin**

- Allows the plugin to notified when Recaf opens new workspaces and closes old ones.

## Compiling the custom plugin

After creating your plugin compile it using `mvn clean package`. This will generate a jar file in the target directory. Copy this into Recaf’s plugin directory.