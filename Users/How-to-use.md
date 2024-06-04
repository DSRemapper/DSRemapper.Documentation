# How to Use Guide

## Installing DSRemapperApp
The installation process, unless an installer is implemented, is simply as getting a copy of the program from [this GitHub repository](https://github.com/DSRemapper/DSRemapperApp) (on [Release section](https://github.com/DSRemapper/DSRemapperApp/releases)) and un compress it on any location on your computer.

For the moment, **admin privileges are not required for installing or running the program**. If you need them for some reason consult [Admin Privileges section](#admin-privileges)


## Installing Plugins

This can be installed simply downloading and placing them on one of the following folder:
- `[DSRemapper App folder]/Plugins` folder (Folder located on the program folder)
- `[User Documents folder]/DSRemapper/Plugins` folder (Folder located on the users document folder)

When the app is opened, DSRemapper Framework will scan this folders and load any valid plugin on this folders.

### Plugins with errors
If an error occurs with any plugin, DSRemapper App can crash, throw an unexpected error or automatic close.  

You can check the app log files to try to find the problematic plugin (normally will be in the latests log entries), and remove it or try to contact the developer of the plugin to fix the error (unless you are the developer of it; in that case, fix it).

### What happens if no plugins are installed?
The DSRemapper Framework requires plugins to work. If they are not provided to the app, will be nothing more than a "good looking" and empty interface that does nothing.

_**The minimum required plugins are:** one Input plugin, one Remapper plugin and one Output plugin_

_Note: There may be some all-in-one "Input" plugins, which can do everything without needing a Remapper and/or Output plugin._


## Using the program
You only need to open it. When it's open and all plugins are loaded, you will see all detected physical controllers on a list view. There you can select a profile (script) to remap the physical controller to virtual ones.

### Profiles
Profiles are scripts stored on `[User Documents folder]/DSRemapper/Profiles` folder. This can be scripts written on a programming language or some sort of instructions that can be interpreted by a Remapper plugin.

_Note: Only supported file extensions will be showed. Supported extensions depends on loaded Remapper plugins. (for example, if Lua Remapper plugin is loaded, `.lua` files will be showed on the profile list)_

### Admin privileges
The program is meant to not require admin privileges _(and I try my best to keep it in that way)_. If these are required for any reason, is at your own risk and you should consider these [items on Risks section](#risks-of-admin-privileges).

_**Disclaimer:** The DSRemapper is licensed under MIT license, which offers no guaranties or liability. I'm not responsible for what you do with the program or what the program can do if, somehow, malicious code is injected on it.  
I will try to do my best to prevent this for happening, but I want the program to offer a liberty which comes with this costs._

_**I don't want to scare any user, but I recognize my program can be harmful if an unexperienced user, or inclusive experienced users, use it without knowing what they are doing.**  
Hackers, cyber criminals and malicious persons exists and I can't do anything about it._

#### Vulnerabilities
_This section only applies to DSRemapper App, Framework and any plugin I develop and is published on [DSRemapper GitHub Organization](https://github.com/DSRemapper)._

If any vulnerability is detected, you can raise a issue, on the respective repository, to inform of it. _This is no warranty of it to be solved_. DSRemapper is intended to have this permissive behavior and will be responsibility of the users to prevent the program from having unexpected behavior.

_Note: If the vulnerability is generated for normal program function I will not be considered as a vulnerability issue._

#### Risks of admin privileges
- DSRemapper Framework loads plugins written with .NET Framework (C#, Visual Basic, etc.) which can have functions for plugin setup, which executes on plugin load. If this functions have malicious code, these functions will be execute without any warning or confirmation. **(Be sure from where you download the plugins, use only thrusted sources)**
- Some Remapper plugins can load scripts written with a programming language (Lua, for example) which can execute malicious instructions. **(Try to write the plugins yourself. If you download it from internet verify it before using it)**
