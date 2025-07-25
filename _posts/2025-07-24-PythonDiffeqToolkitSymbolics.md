---
title: "Using the Python Differential Equations Toolkit - Symbolics"
date: 2025-07-24 12:00:00
categories: [general]
tags: ["DifferentialEquations","Python"]
published: true
---



If you haven't already, make sure that you have set up a Python virtual environment, and have installed SymPy.

## Using the toolkit: Symbolics

In this section, we will use Sympy to solve the differential equation

$$
\frac{dx}{dt} = t^2 x^2.
$$

Start by navigating to your virutal environment's directory, activating the virtual environment, and launching the Python interpreter. Import the parts of SymPy that we need:

```python
Python 3.8.10 (tags/v3.8.10:3d8993a, May  3 2021, 11:48:03) [MSC v.1928 64 bit (AMD64)] on win32
Type "help", "copyright", "credits" or "license" for more information.
>>> from sympy import Function, symbols, Eq, dsolve
```

Now declare <code>x</code> to be a symbolic function:

```python
>>> x = Function('x')
```

and declare <code>t</code> to be a symbol:

```python
>>> t = symbols('t')
```

Then input the differential equation:
```python
>>> diffeq = Eq(x(t).diff(t), t**2 * x(t)**2)
```

and use dsolve to solve the differential equation symbolically.

```python
>>> dsolve(diffeq, x(t))
Eq(x(t), -3/(C1 + t**3))
```

According to SymPy, the solution of our differential equation is
$$
x(t) = \frac{-3}{C_1 + t^3}
$$

Where $C_1$ is a free parameter. (P.S. check that this solution works by hand). Now suppose we want to find a particular solution by introducing an initial condition:

$$
x(0) = 1
$$

We can define this initial condition by inputting <code>initial_condition = {x(0): 1}</code>

```python
>>> initial_condition = {x(0): 1}
```

Now we can solve this initial value problem with dsolve but including the initial condition:

```python
>>> dsolve(diffeq, x(t), ics=initial_condition)
Eq(x(t), -3/(t**3 - 3))
```

SymPy computer that the solution of this initial value problem is 

$$
x(t) = \frac{-3}{t^3 - 3}.
$$

```python
Python 3.8.10 (tags/v3.8.10:3d8993a, May  3 2021, 11:48:03) [MSC v.1928 64 bit (AMD64)] on win32
Type "help", "copyright", "credits" or "license" for more information.
>>> from sympy import Function, symbols, Eq, dsolve
>>> x = Function('x')
>>> t = symbols('t')
>>> diffeq = Eq(x(t).diff(t), t**2 * x(t))
>>> dsolve(diffeq, x(t))
Eq(x(t), -3/(C1 + t**3))
>>> initial_condition = {x(0): 1}
>>> dsolve(diffeq, x(t), ics=initial_condition)
Eq(x(t), -3/(t**3 - 3))
```