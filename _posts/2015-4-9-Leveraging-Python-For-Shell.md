---
layout: post
title: Leveraging Python for Basic Shell Commands
---

I love Python. And I love Shell scripts too. But Python, definitely more. I spend 80% of my time on my MBP in the terminal. And being a student with some administrative responsibilities, I frequently have to perform certain simple tasks (creating directory structures, files etc.) numerous times. To that extent I find that Python provides a lot of tools that one can use to efficiently do such shell tasks.

### Scenario

I have a folder structure that looks something like this:

```sh
tester
├── student_scripts
│   ├── student_1
│   ├── student_2
...
```
And I want to create a directory structure like this:

```sh
H2
├── studentfolder_1
│   ├── grades
│   ├── studentout
│   └── testerout
├── studentfolder_2
│   ├── grades
│   ├── studentout
│   └── testerout
|   some_other_random_files
|   and_some_more_random_files
...
```

And I have close 50 student folders. My problem is how do I take something as simple as a `mkdir` command and automatically create the required folder structure without
- manually entering the student names
- writing a complex shell script

### Solution
1. __Create a Python script__: Let's call it `tester/tmp/listdir.py` (Yes I'm not very creative with names). Here's what it looks like:

```python
import os
from os import path
root = path.dirname(path.realpath(__file__+"/.."))
root = path.join(root, "student_scripts")
for folder in os.listdir(root):
    if path.isdir(path.join(root, folder)):
        print folder+"/testerout"
        print folder+"/studentout"
        print folder+"/grades"
```
1. __Create the folder structure__: Next we use a neat feature of [Shell Expansion](http://tldp.org/LDP/Bash-Beginners-Guide/html/sect_03_04.html), Command Substitution. Next enter the following command in the terminal:

```sh
$ mkdir H2
$ mkdir -p `python ~/dev/personal/h2_tester/tmp/listdir.py`
```

And that's it. Finito. Folder structure is created.

### My experience with Python
I am definitely not an expert on Python to comment on the powers of python. But, I can tell you this. It is brilliant. In just 5 lines of dead simple code, I achieved something that would have involved some pain staking StackOverflow browsing for shell scripts or manual labor. Didn't have to do any of it.

I am not asking you convert to only Python for your scripts from now on, but you can use the power of python scripts to augment your shell tasks. Definitely worth a try.
