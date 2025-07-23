---
title: "The Python Differential Equations Toolkit (Windows)"
date: 2025-07-20 12:00:00
categories: [general]
tags: ["DifferentialEquations","Python"]
published: true
---
[winlogo]: https://i.sstatic.net/Rfuw7.png
[newwinlogo]: https://i.sstatic.net/B8Zit.png
[oldwinlogo]: https://i.sstatic.net/T0oPO.png

To solve differential equations in Python, we will use a trio of Python libraries: SymPy, SciPy, and Matplotlib. This page gives instructions on how to set up a virtual environment to use these libraries on Windows. After following the instructions on this page, you should be able to:

- Create a virtual environment using venv
- Install SymPy, SciPy, and Matplotlib into your new virtual environment using pip
- Write a short program using those libraries to solve a simple ODE both symbolically and numerically, and plot the solution on a graph.

## Setting up the virtual environment
This section gives instructions on how to set up a python "virtual environment" using *venv* on Windows. The purpose of a virtual environment is to avoid clashes of libraries and dependencies, and to avoid installing them globally onto your system. This makes sure that you're using the same version of your libraries every time you work on your project.


{:start="1"}
1. Open the command prompt. You can do this by pressing  <kbd>Windows</kbd> + <kbd>R</kbd>, or going to the start menu and searching "cmd".

2. Check if python is installed. Type <code>python --version</code>. You should get something like this:

```bat
C:\Users\me>python --version
Python 3.8.10
```

    If, instead, you see:

```bat
C:\Users\me>python --version
'python' is not recognized as an internal or external command,
operable program or batch file.
```

then you need to download and install python from [python.org/downloads](https://www.python.org/downloads/).  After downloading and installing, try printing the python version again.

{:start="3"}
3. Now that you have Python installed, you are going to create a virtual environment using *venv*. A virtual environment is a private workspace for a specific project. venv is a module that comes bundled with every python installation. To create the virtual environment, first navigate to the documents folder by using the cd ("change directory") command <code>cd Documents</code>: 

```bat
C:\Users\me>python --version
Python 3.8.10

C:\Users\me>cd Documents
```

Now we are going to run the built-in venv command as a module, and tell it to create a virtual environment called diffeq. Type into the command prompt <code>python -m venv diffeq </code>:

```bat
C:\Users\me>python --version
Python 3.8.10

C:\Users\me>cd Documents

C:\Users\me\Documents>python -m venv diffeq
```

Now navigate into the virtual environment directory with the cd command, <code>cd diffeq</code>:

```bat
C:\Users\me>python --version
Python 3.8.10

C:\Users\me>cd Documents

C:\Users\me\Documents>python -m venv diffeq

C:\Users\me\Documents>cd diffeq
```

Finally, to activate the virtual environment, type <code>Scripts\Activate.bat</code>:

```bat
C:\Users\me>python --version
Python 3.8.10

C:\Users\me>cd Documents

C:\Users\me\Documents>python -m venv diffeq

C:\Users\me\Documents>cd diffeq

C:\Users\me\Documents\diffeq>Scripts\Activate.bat
```

Now your next line should have the name of virtual environment in parenthesis, like:

```bat
C:\Users\me>python --version
Python 3.8.10

C:\Users\me>cd Documents

C:\Users\me\Documents>python -m venv diffeq

C:\Users\me\Documents>cd diffeq

C:\Users\me\Documents\diffeq>Scripts\Activate.bat

(diffeq) C:\Users\me\Documents\diffeq>
```

Whenver we are using our diffeq toolkit (including when we install packages) we will want to have the virtual environment activated. To exit the virtual environment, simply type <code>deactivate</kbd>:

```bat
C:\Users\me>python --version
Python 3.8.10

C:\Users\me>cd Documents

C:\Users\me\Documents>python -m venv diffeq

C:\Users\me\Documents>cd diffeq

C:\Users\me\Documents\diffeq>Scripts\Activate.bat

(diffeq) C:\Users\me\Documents\diffeq>deactivate
C:\Users\me\Documents\diffeq>
```



## Gathering your libraries
So far our virtual environment doesn't have the libraries we need for our toolkit. In this section, we will install SymPy, SciPy, and Matplotlib into our virtual environment.

1. Open the command prompt and navigate to your virtual environment directory by typing

```bat
cd C:\Users\me\documents\diffeq
```

and activate the virtual environment by typing

```bat
\Scripts\Activate.bat
```

Now that we have the virtual environment active, we will install our libraries using pip. pip is software that comes bundled with every python distribution. With your virtual environment, type the following to install SymPy:

```bat
pip install sympy
```

If asked, enter <kbd>Y</kbd> to allow the installation of dependencies.

Similarly, install scipy and matplotlib with

```bat
pip install scipy
pip install matplotlib
```
and again install any dependencies you don't currently have (for example, the numpy python package is required for scipy).

Now that you have your main libraries installed, you need to check that you can import and use them in a python program. To launch the python interpreter, simply type:

```bat
python
```

and you will be greeted with something like

```python
Python 3.8.10 (tags/v3.8.10:3d8993a, May  3 2021, 11:48:03) [MSC v.1928 64 bit (AMD64)] on win32
Type "help", "copyright", "credits" or "license" for more information.
>>>
```

Now check that Sympy, Scipy, and Matplotlib are properly installed. With the python interpreter active, type:

```python
>>> import sympy
>>> print(sympy.__version__)
```

you should see the version of sympy printed to the console. if however, you get:

```python
>>> import sympy
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
ModuleNotFoundError: No module named 'sympy'
```

then you don't have access to the sympy module. One thing to check is that the you activated the virtual environment before starting the python interpreter. Another reason could be that your installation of sympy failed.

Similarly, check that scipy and matplotlib were installed into the virtual environment:

```python
>>> import scipy
>>> import matplotlib
>>> print(scipy.__version__)
>>> print(matplotlib.__version__)
```

When you're done, exit the python interpreter by typing:

```python
>>> quit()
```

## Using the toolkit: Symbolics

In this section, we will use Sympy to solve the differential equation

$$
\frac{dx}{dt} = t^2 x^2.
$$

Start by navigating to your virutal environment's directory, and activating the virtual environment, and launching the Python interpreter. epxImport the parts of SymPy that we need:

```python
Python 3.8.10 (tags/v3.8.10:3d8993a, May  3 2021, 11:48:03) [MSC v.1928 64 bit (AMD64)] on win32
Type "help", "copyright", "credits" or "license" for more information.
>>> from sympy import Function, symbols, Eq, dsolve
```

Now declare x to be a symbolic function:

```python
Python 3.8.10 (tags/v3.8.10:3d8993a, May  3 2021, 11:48:03) [MSC v.1928 64 bit (AMD64)] on win32
Type "help", "copyright", "credits" or "license" for more information.
>>> from sympy import Function, symbols, Eq, dsolve
>>> x = Function('x')
```

and declare t to be a symbol:

```python
Python 3.8.10 (tags/v3.8.10:3d8993a, May  3 2021, 11:48:03) [MSC v.1928 64 bit (AMD64)] on win32
Type "help", "copyright", "credits" or "license" for more information.
>>> from sympy import Function, symbols, Eq, dsolve
>>> x = Function('x')
>>> t = symbols('t')
```

Then input the differential equation:
```python
Python 3.8.10 (tags/v3.8.10:3d8993a, May  3 2021, 11:48:03) [MSC v.1928 64 bit (AMD64)] on win32
Type "help", "copyright", "credits" or "license" for more information.
>>> from sympy import Function, symbols, Eq, dsolve
>>> x = Function('x')
>>> t = symbols('t')
>>> diffeq = Eq(x(t).diff(t), t**2 * x(t)**2)
```

and use dsolve to solve the differential equation symbolically.
```python
Python 3.8.10 (tags/v3.8.10:3d8993a, May  3 2021, 11:48:03) [MSC v.1928 64 bit (AMD64)] on win32
Type "help", "copyright", "credits" or "license" for more information.
>>> from sympy import Function, symbols, Eq, dsolve
>>> x = Function('x')
>>> t = symbols('t')
>>> diffeq = Eq(x(t).diff(t), t**2 * x(t))
>>> dsolve(diffeq, x(t))
Eq(x(t), -3/(C1 + t**3))
```

According to SymPy, the solution of our differential equation is
$$
x(t) = \frac{-3}{C_1 + t^3}
$$

Where $C_1$ is a free paramter. (P.S. check that this solution works by hand).

## Using the Toolkit: Numerics
