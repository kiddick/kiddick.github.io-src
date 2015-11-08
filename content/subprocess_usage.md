Title: Subprocess usage
Date: 2015
Modified: 2015
Category: Python
Tags: python, subprocess

Let's view several cases.

<a href="https://docs.python.org/2/library/subprocess.html#subprocess.call" target="_blank">subprocess.call(args, *, stdin=None, stdout=None, stderr=None, shell=False)</a>


|args|shell|executable|result|
|---|---|---|---|---|
|'ls -l'|False|ls -l|exception [Errno 2] No such file or directory|
|'ls -l'|True|/bin/sh|OK|
|['ls', '-l']|False|ls|OK|
|['ls', '-l']|True|/bin/sh|only first command (ls) will be executed|

Source code:

```python
import subprocess

args = 'ls -l'  # string
try:
    subprocess.call(args, shell=False)
except Exception, e:
    print str(e)

args = 'ls -l'  # string
subprocess.call(args, shell=True)

args = ['ls', '-l']
subprocess.call(args, shell=False)

args = ['ls', '-l']
subprocess.call(args, shell=True)
```