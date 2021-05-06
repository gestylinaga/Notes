# Glossary
by: [Gesty Linaga](https://github.com/gestylinaga/)

## String Concatenation
- aka 'how to glue strings together'

> **f strings**
> - used to automatically concatenate different data types together
> - only works in python3
> ```python
> x = 452
> print(f"this text with {x}! ")
> ```

## Variables 
- containers for storing values in your code
    - in python "dynamically typed" as opposed to "static typing"

```python
variable_name = 'text string'
variable_name2 = 8
```

> **Naming Convention** 
> - generally agreed upon naming scheme in python
>     - with_underscores_like_this
>     - OrWithAlternatingCapsLikeThis
> - **Reserved Words:** can't be used in variable names
>     - ie: and, except, lambda, if, import, etc...

## Functions
- Blocks of code (logic in code) that do something more complex to avoid repetitive logic
    - defined using 'def' keyword
    - only runs when called
        - calling a function = to execute the function
        - () = calls function

```python
def function_name_1():
    print('look at this function')

function_name_1()
```

> **Parameters**
> - aka arguments; a way to pass info to functions
> ```python
> calculation_to_hours = 24
> name_of_unit = "hours"
> 
> def days_to_units(num_of_days, custom_message):
>     print("f{num_of_days} days are {num_of_days * calculation_to_hours} {name_of_unit}")
>     print(custom_message)
> 
> 
> days_to_units(35, 'look at this number')
> days_to_units(70, "look at this custom message")
> days_to_units(420, "loool")
> ```


## Scope
- variable scopes in functions
- a variable is only available inside the region it is created
    - Global Scope = variables available within any scope
    - Local Scope = variables created inside function
        - can only be used inside function

```python
variable_global = 'this works across the whole thing'

def sample_function_1():
    variable_local = 'this only works in function 1'

def sample_function_2():
    variable_local = 'this only works in function 2'

```

## User Input
```python
input()
```
- Built-In function provided by Python itself
- asks the user for input
- Python stops executing when it comes to the input()

```python
input("give me an input \n")
```
> gets user input and adds a line break

```python
user_input = input("give me an input \n")
```
> saves input as new variable 'user_input'

> **Return Values**
> - A function can *return* data as a result
> ```python
> return f"{num_of_days} days are {num_of_days * calculation_to_hours} {name_of_unit}"
> ```
