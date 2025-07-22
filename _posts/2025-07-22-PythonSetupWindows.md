---
title: "Setting Up the Python Differential Toolkit (Windows)"
date: 2025-07-20 12:00:00
categories: [general]
tags: [DifferentialEquations]
author: Matthew
published: true
---

# Setting up the Python Toolkit (Windows)

1. Open the command prompt. You can do this by pressing WindowsKey + R, or going to the start menu and searching "cmd",

2. Check if python is installed. Type

```console
python --version
```

You should get something like this

```console
Python 3.8.10
```

If, instead, you see

```console
'python' is not recognized as an internal or external command,
operable program or batch file.
```

then you need to download and install python from [python.org/downloads](https://www.python.org/downloads/).  After downloading and installing, try printing the python version again.

{:start="3"}
3. Now that you have Python installed, you are going to create a virtual environment using *venv*. A virtual environment is a private workspace for a specific project. For us, that project is the collection of class assignments.

To create the virtual environment, first enter the documents folder by using the cd ("change directory") command: 

```console
cd Documents
```

Now we are going to run the built-in venv command as a module, and tell it to create a virtual environment called diffeq. Type into the command prompt:

```console
python -m venv diffeq
```

To actiave the virtual environment, type:

```console
diffeq\Scripts\Activate.bat
```

Now your next line should look like:

```console
(diffeq) C:\Users\user\Documents>
```

Whenver we are using our diffeq toolkit, we will want to have the virtual environment activated. 


