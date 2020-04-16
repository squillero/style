# Python

> **Notez Bien**: All these rules are meant to be broken, **BUT** you need a very good reason **AND** you must explain it in a comment.

## Style

### Names (TL;DR)

* `module_name`, `package_name`, `ClassName`, `method_name`, `ExceptionName`, `function_name`, `GLOBAL_CONSTANT_NAME`, `global_var_name`, `instance_var_name`, `function_parameter_name`, `local_var_name`.

### General

* Use nouns for variables, full sentences for functions (`factors = factorize(formula)`); predicates (i.e., functions returning a boolean value) should start with the `is_` prefix (`if is_gargled(quz):`).

* Prefer an f-string (a.k.a. formatted string literal) over an explicit formatting operation or the string interpolation operator (`f"v={foo}"` instead of `"v={}".format(foo)` or `"v=%s" % (foo,)`). Use single quotes for string constants such as function parameters and dictionary keys (`'utf-8'` or `data['foo']`); use double quotes for messages to the user (`logging.warning(f"data: {data['bar']}")`).

* Start names internal to a module with a single underscore (`_`).

* Define `__all__` when a file is a collection of functions.

* Use `assert` to check the internal consistency and verify the correct usage of methods, not to check for the occurrence of unexpected events. That is: The optimized bytecode should not waste time verifying the correct invocation of methods or running sanity checks.

* Complex compound statements (i.e., multiple statements on the same line) should be avoided. However, a second statement on the same line of a simple `if` can sometimes improve readability (`if value is None: return True`).

* Annotate all functions (refer to [PEP-483](https://www.python.org/dev/peps/pep-0483/) and [PEP-484](https://www.python.org/dev/peps/pep-0484/) for details).

* Format source code using [Yapf](https://github.com/google/yapf)'s style `"{based_on_style: google, column_limit=120, blank_line_before_module_docstring=true}"`

* Follow [PEP-440](https://www.python.org/dev/peps/pep-0440/) for version identification.

### Classes

* Start names private or protected within a class with a single underscore (`_`); don't dunder (`__`).

* Name properties as variables; methods as functions (`foo.factors = bar.factorize(baz.formula)`).

* Do not implement getters and setters, use properties instead. Whether a function does not need parameters consider using a property (`foo.first_bar` instead of `foo.calculate_first_bar()`). However, do not hide complexity: if a task is computationally intensive, use an explicit method (`big_number.get_prime_factors()`). 

* Do not override `__repr__`.

* Explicitly derive container classes from `collections.abc`.

* Override `__getstate__` and `__setstate__` if you define `__slots__`; write these functions in the very beginning of the class, before `__init__`. Define `__slots__` only if you are really confident about it.

### Comments

* Explain the purpose of all functions and classes in docstrings; be verbose when needed, otherwise use single-line descriptions (note: each verbose description also includes a concise one as its first line). Be terse describing methods, but verbose in the class docstring, possibly including usage examples. Comment public attributes and properties in the `Attributes` section of the class docstring (even though PyCharm is not supporting it, yet); don't explain basic customizations (e.g., `__str__`). Comment `__init__` only when its parameters are not obvious. Use the formats suggested in the [Google's style guide](https://google.github.io/styleguide/pyguide.html&#35;383-functions-and-methods).

* Use English for names, in docstrings and in comments. Favor formal language over slang, wit over humor, and American English over British.

## Conventions

### Paranoid classes

`Paranoid` classes implement `run_paranoia_checks()`.

```python
class Paranoid(ABC):
    def run_paranoia_checks(self) -> bool:
        raise NotImplementedError
```

The functions named `run_paranoia_checks` perform sanity checks. They always return `True`, but stop the execution throwing an exception as soon as an inconsistency is detected. The functions are not supposed to be called in production environments (i.e., when `-O` is used). Hint: it is safe to use `assert some_object.run_paranoia_checks()`. 

### Pedantic classes

`Pedantic`classes implement `is_valid(obj)`.

```python
class Pedantic(ABC):
    def is_valid(self, obj: Any) -> bool:
        raise NotImplementedError
```

The functions named `is_valid` checks an object against a specification (e.g., an object against its semantic, an element inside a collection). They return either `True` or `False`. Hint: sometimes it could be useful to inlude them into `run_paranoia_checks`:

```python
def run_paranoia_checks(self):
    assert self.is_valid(self.value), "Meaningful message"
    return True
```
