---
title: "The Python Differential Equations Toolkit (Windows)"
date: 2025-07-20 12:00:00
categories: [general]
tags: [DifferentialEquations]
author: "Matthew Sutter"
published: true
---
[winlogo]: https://i.sstatic.net/Rfuw7.png
[newwinlogo]: https://i.sstatic.net/B8Zit.png
[oldwinlogo]: https://i.sstatic.net/T0oPO.png
This page give beginner instructions on how to set up python to solve differential equations in Python, on Windows. After following these instructions, you should be able to 

1. Create a virtual environment using venv
2. Install SymPy, SciPy, and Matplotlib into your new virtual environment using pip
3. Write a short program using those libraries to solve a simple ODE both symbolically and numerically, and plot the solution on a graph.

## Setting up the virtual environment
This section gives instructions on how to set up a python "virtual environment" using *venv* on Windows. The purpose of a virtual environment is to avoid clashes of libraries and dependencies, and to avoid installing them globally onto your system. This makes sure that you're using the same version of your libraries every time you work on your project.


{:start="1"}
1. Open the command prompt. You can do this by pressing  <kbd>![Windows Key][newwinlogo]</kbd> + R, or going to the start menu and searching "cmd".

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
3. Now that you have Python installed, you are going to create a virtual environment using *venv*. A virtual environment is a private workspace for a specific project. venv is a module that comes bundled with every python installation.

To create the virtual environment, first navigate to the documents folder by using the cd ("change directory") command: 

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

Now that we have the virtual environment active, we will install our libraries using pip. pip is software that comes bundled with every python distribution. With your virtual environment, type the following to install SymPy:

```console
pip install sympy
```

If asked, enter <code>Y</code> to allow the installation of dependencies.

Similarly, install scipy and matplotlib with

```console
pip install scipy
pip install matplotlib
```
and again install any dependencies you don't currently have (for example, the numpy python package is required for scipy).

Now that you have your main libraries installed, you need to check that you can import and use them in a python program. To launch the python interpreter, simply type:

```console
python
```

and you will be greeted with something like