---
title: "Using the Python Differential Equations Toolkit - Numerics"
date: 2025-07-24 12:00:00
categories: [general]
tags: ["DifferentialEquations","Python"]
published: true
---

If you haven't already, make sure that you have set up a Python virtual environment, and have installed Scipy.

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

