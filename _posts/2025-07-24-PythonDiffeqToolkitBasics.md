---
title: "Using the Python Differential Equations Toolkit - Basics"
date: 2025-07-24 12:00:00
categories: [general]
tags: ["DifferentialEquations","Python"]
published: true
---

If you haven't already, make sure that you have set up a Python virtual environment, and have installed SymPy, SciPy, and Matplotlib. 


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
Python 3.8.10 (tags/v3.8.10:3d8993a, May  3 2021, 11:48:03) [MSC v.1928 64 bit (AMD64)] on win32
Type "help", "copyright", "credits" or "license" for more information.
>>> from sympy import Function, symbols, Eq, dsolve
>>> x = Function('x')
```

and declare <code>t</code> to be a symbol:

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

Where $C_1$ is a free parameter. (P.S. check that this solution works by hand). Now suppose we want to find a particular solution by introducing an initial condition:

$$
x(0) = 1
$$

We can define this initial condition by inputting <code>initial_condition = {x(0): 1}</code>

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
```

Now we can solve this initial value problem with dsolve but including the initial condition:

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

SymPy computer that the solution of this initial value problem is 

$$
x(t) = \frac{-3}{t^3 - 3}
$$

## Using the toolkit: Numerics

In this section, we will use SciPy to numerically solve our differential equation (IVP)

$$
\frac{dx}{dt} = t^2 x^2, \quad x(0)=1
$$

Activate your virtual environment, launch the Python interpreter, and import integrate from scipy:

```python
Python 3.8.10 (tags/v3.8.10:3d8993a, May  3 2021, 11:48:03) [MSC v.1928 64 bit (AMD64)] on win32
Type "help", "copyright", "credits" or "license" for more information.
>>> from scipy import integrate
```

When solving ODEs numerically, scipy assumes that you have an equation of the form:

$$
\frac{dx}{dt} = f(t,x)
$$

where $x$ can be a scalar or a vector. It is our job to define this $f$ function to match our differential equation. We can do this in the following way:

```python
Python 3.8.10 (tags/v3.8.10:3d8993a, May  3 2021, 11:48:03) [MSC v.1928 64 bit (AMD64)] on win32
>>> from scipy import integrate
>>> def f(t,x): return t**2 * x**2
...
>>>
```

when you see the <code>...</code>, simply press enter again to complete the function definition. Next define the initial condition by writing <code>initial_condition = [2]</code>:

```python
Python 3.8.10 (tags/v3.8.10:3d8993a, May  3 2021, 11:48:03) [MSC v.1928 64 bit (AMD64)] on win32
>>> from scipy import integrate
>>> def f(t,x): return t**2 * x**2
...
>>> initial_condition = [2]
```

We still need to give the interval that we're solving the differential equation over. Lets try to find $x(1)$. Since our initial time is $0$, and our final time is $1$, we will define <code>interval = [0,1]</code>:

```python
Python 3.8.10 (tags/v3.8.10:3d8993a, May  3 2021, 11:48:03) [MSC v.1928 64 bit (AMD64)] on win32
>>> from scipy import integrate
>>> def f(t,x): return t**2 * x**2
...
>>> initial_condition = [2]
>>> interval = [0,1]
```

Now we will solve our IVP with scipy.integrate:

```python
Python 3.8.10 (tags/v3.8.10:3d8993a, May  3 2021, 11:48:03) [MSC v.1928 64 bit (AMD64)] on win32
>>> from scipy import integrate
>>> def f(t,x): return t**2 * x**2
...
>>> initial_condition = [2]
>>> interval = [0,1]
>>> integrate.solve_ivp(f, interval, initial_condition)
  message: The solver successfully reached the end of the integration interval.
  success: True
   status: 0
        t: [ 0.000e+00  1.000e-04  1.100e-03  1.110e-02  1.111e-01
             4.951e-01  8.387e-01  1.000e+00]
        y: [[ 2.000e+00  2.000e+00  2.000e+00  2.000e+00  2.002e+00
              2.176e+00  3.297e+00  6.000e+00]]
      sol: None
 t_events: None
 y_events: None
     nfev: 56
     njev: 0
      nlu: 0
```

The <code>t</code> list in the output represents the "mesh" that the numerical calculation was done on, and the <code>y</code> list represents the numerical solution of the IVP at the corresponding <code>t</code> values. Scipy has approximated the solution at <code>t = 1</code> to be <code>y = 6.000e+00</code>. Compare this to our symbolic solution in the previous section, does this make sense?

Now lets try solving the differential equation over a larger interval, say <code>interval=[0,5]</code>, so that we're trying to find $x(5)$.


```python
Python 3.8.10 (tags/v3.8.10:3d8993a, May  3 2021, 11:48:03) [MSC v.1928 64 bit (AMD64)] on win32
>>> from scipy import integrate
>>> def f(t,x): return t**2 * x**2
...
>>> initial_condition = [2]
>>> interval = [0,5]
>>> integrate.solve_ivp(f, interval, initial_condition)  message: Required step size is less than spacing between numbers.
  success: False
   status: -1
        t: [ 0.000e+00  1.000e-04 ...  1.145e+00  1.145e+00]
        y: [[ 2.000e+00  2.000e+00 ...  5.502e+13  1.092e+14]]
      sol: None
 t_events: None
 y_events: None
     nfev: 638
     njev: 0
      nlu: 0
```

Examine the output. What did scipy numerically calculate $x(5)$ to be? Can you explain why scipy returned <code>success: False</code>? What happened here that is different than with the previous interval?

## Using the toolkit: Matplotlib

In this section, we will use Matplotlib to plot some solutions of differential equations.

