---
title: "Setting Up the Python Differential Toolkit (Windows)"
date: 2025-07-20 12:00:00
categories: [general]
tags: [DifferentialEquations]
author: "Matthew Sutter"
published: true
---


## Setting up the virtual environment
This section gives instructions on how to set up a python "virtual environment." The purpose of a virtual environment is to avoid clashes of libraries and dependencies, and to avoid installing them globally onto your system. This makes sure that you're using the same version of your libraries every time you work on your project.

----
1. Open the command prompt. You can do this by pressing WindowsKey + R, or going to the start menu and searching "cmd".

2. Check if python is installed. Type:

```console
python --version
```

You should get something like this:

```console
Python 3.8.10
```

If, instead, you see:

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

Now we are going to run the built-in venv command as a module, and tell it to create a virtual environment called diffeq. Type into the command prompt (using whatever version of python you have installed):

```console
python3.8.10 -m venv diffeq
```

By calling the specific version of python, we will ensure that whenever we go back to our project, the same version of python is used. Now navigate into the virtual environment directory with the cd command:

```console
cd diffeq
```

Finally, to activate the virtual environment, type:

```console
\Scripts\Activate.bat
```

Now your next line should have the name of virtual environment in parenthesis, like:

```console
(diffeq) C:\Users\me\Documents>
```

Whenver we are using our diffeq toolkit (including when we install packages) we will want to have the virtual environment activated. To exit the virtual environment, simply type:

```console
deactivate
```


## Gathering your libraries
So far our virtual environment doesn't have the libraries we need for our toolkit. In this section, we will install SymPy, SciPy, and Matplotlib into our virtual environment.

1. Open the command prompt and navigate to your virtual environment directory by typing

```console
cd C:\Users\me\documents\diffeq
```

and activate the virtual environment by typing

```console
\Scripts\Activate.bat
```

Now that we have the virtual environment active, we will install our libraries using pip. pip is software that comes bundled with every python distribution.

