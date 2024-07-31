# Building abstractions with functions

Computing is representing information, specifying logic for how to process it, and designing abstractions to manage the complexity of the logic.

Composing Programs uses Python because the language has i) emphasized the human interpretability of Python code and ii) is multiparadigm.

## Expressions and Statements

Broadly speaking, computer programs are composed of instructions to:

1. Compute a value
2. Execute an action

An expression computes values: the combination of data (e.g. variables, literals) and logic (e.g. functions, methods) that resolves to a value.

A statement executes an action that don't necessarily compute a value. For example, statements include:

- Variable assignment
- Conditional operation
- Function calls
- `for` or `while` Loops

## Elements of programming

Programming languages are a i) framework within which to organize our ideas of computational processes and ii) communicate those ideas to humans.

Every language has 3 mechanisms to combine simple ideas to form more complex ideas:

1. Primitive expressions and statements: a language's simplest building block
2. Means of combination: compound elements are built from simpler ones
3. Means of abstraction: compound elements can be named and manipulated as units

In programming we deal with 2 elements: data and functions (which is really also data).

1. Data is values we want to manipulate
2. Functions are the rules for manipulating the data

Thus, all programming languages must describe primitive data and functions, and have methods to combine and abstract functions and data.

### Expressions

A primitive expression can be a number (e.g. in base 10).

```python
# Example expression
37
```

A compound expression can be numbers combined with mathematical operators using **infix** notation (where the operator appears in between the operands).

```python
# Example compound expression in infix notation
3 + 2
```

### Call expressions

A call expression applies a function to some arguments. A function (in algebra) is a mapping from input arguments to an output value.

In call expressions, the operator is the function name preceding the parentheses enclosing the list of operand expressions.

```python
# Compound expression where the operator `max` operates on the operands `1` and `2`
max(1, 2)
```

Function notation has 3 advantages over infix notation:

1. They can take an arbitrary number of arguments
2. Nesting expressions is explicit in function, but not infix, notation

```python
# Explicit nesting with function notation
max(min(3, 2), min(4, 7))

# Implicit nesting with infix notation
12 * 2 + 4 / 5
```

For example, the `add` function is equivalent to the `+` operator — they both add 2 numbers.

3. Function notation is simpler to name than infix notation (which can require symbols that are hard to type)

### Importing library functions

Python organizes functions and data into modules that belong to the Python library. We need to import modules to use the function and data they export.

```python
# Importing the `math` module to use its `sqrt` function
import math
math.sqrt(4)
```

An import statement i) designates a module name (e.g. `math`, `operator`) and then ii) lists the named attribute that the module imports (the module or a elements of the module).

### Names and the environment

If a value has been given a name we say that the name **binds to the value**.

We can create new bindings with the assignment operator `=`:

```python
# Some assignment statements
radius = 10
length = 5 * 2
```

Names are also bound via `import` statements:

```python
>>> pi = 10
>>> pi
10
>>> from math import pi
>>> pi
3.141592653589793
```

If we bind names to values the interpreter needs to store those bindings somewhere to keep track of the names, values, and bindings. This somewhere is called an **environment**.

Names are also bound to functions as well as values. Unlike values, Python renders functions as their identifying description:

```python
>>> max
<built-in function max>
```

We can use assignment statements to bind new names to functions

```python
>>> x = max
>>> x
<built-in function max>
```

When a name is bound to a new value through an assignments it stops being bound to its previous value. Even built-in names can be bound to new values:

```python
>>> max = 5
>>> max
5
>>> from builtins import max
>>> max
<built-in function max>
```

When executing an assignment statement Python first evaluates the expression on the right side before changing the binding of the name to the left with the expression on the right. This is why assignment statements can handle complex expressions: because they wait for the expression to evaluate before binding the name and resulting value.

Python also supports the assignment of multiple names in a single line.

```python
a, b, c = "a", "b", "c"
```

However, all expressions on the right side are evaluated before the names are bound to the result of the expressions. This is why we can swap values in Python in the same line:

```python
>>> x, y = 1, 2
>>> x, y = y, x
>>> x
2
>>> y
1
```

### Evaluating nested expressions

Interpreters follow a recursive process to evaluate nested call expressions:

1. Evaluate what is the operator (function) and what are the inputs to the operator (the operand subexpressions), and then
2. Apply the function to the operands

This procedure is recursive because to apply the function to its arguments we first need to evaluate the result of the subexpressions, which are themselves operators and operands.

Step 1 means that to evaluate a call expression we must first evalue its subexpressions.

Thus, the evaluation procedure — this process of evaluating nested call expressions — is recursive because you need the same methodology to invoke itself to evaluate the expression.

The repeated application of step 1 means that we need to evaluate primitive expressions like i) a numeral `2` that evalues to the number `2` or ii) a name like `add` to call the function its bound to.

A name evaluates to the value associated with that name in the current environment. Environments provide the context in which execution takes place and we can't understand the program execution without the environment.

E.g. we can't understand:

```python
# The subexpression `x+1` needs to evaluate
# before evaluating `sqrt` and the result of `x+1`
sqrt(x+1)
```

Without information from the environment about the value of `sqrt` and `x`.

Statements are executed, not evaluated. Thus, statements make a change rather than produce a value.

### Non-pure print function

**Pure** functions need to satisfy 2 requirements:

1. They have no side effects
2. Given the same inputs they return the same outputs

E.g., functions like `abs`, `min` and `max` are pure because they have no side effects and only return their output values.

**Non-pure** functions not only return and output but have side effects.

E.g., `print` writes to `stdout` as well as returning `None`:

```python
>>> print(print(1), print(2))
1
2
None None
```

While pure functions are more restrictive because they don't have side effects, they're more valuable because:

1. They can be composed more reliably into compount call expressions (because it has no side effects and always applies the same logic to the input)
2. Pure functions are simpler to test
3. Pure functions are essential for writing concurrent programs where call expressions are evaluated simultaneously
