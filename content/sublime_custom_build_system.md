Title: Custom Sublime Text build system for python on Fedora 22
Date: 2015
Modified: 2015
Category: Sublime Text
Tags: sublime text, build system

We need to configure custom build system in Sublime Text. The main requirement is possibility to execute code in new window.

Let's create new build system.

Tools > Build System > New Build System...

Configuration is below.

```python
{
    "cmd": ["gnome-terminal", "-x", "bash", "-c", "python $file; read"], # run new terminal
    "shell": false,
} 
```