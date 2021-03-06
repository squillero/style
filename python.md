# Python

> **Notez Bien**: All these rules are meant to be broken, **BUT** you need a very good reason **AND** you must explain it in a comment.

## Style

### Names (TL;DR)

* `module_name`, `package_name`, `ClassName`, `method_name`, `ExceptionName`, `function_name`, `GLOBAL_CONSTANT_NAME`, `global_var_name`, `instance_var_name`, `function_parameter_name`, `local_var_name`.

### General

* Use nouns for variables, full sentences for functions (`factors = factorize(formula)`); predicates (i.e., functions returning a boolean value) should start with the `is_` prefix (`if is_gargled(quz):`).

* Prefer an f-string (a.k.a. formatted string literal) over an explicit formatting operation or the string interpolation operator (`f"v={foo}"` instead of `"v={}".format(foo)` or `"v=%s" % (foo,)`). Use single quotes for string constants such as function parameters and dictionary keys (`'utf-8'` or `data['foo']`); use double quotes for messages to the user (`logging.warning(f"data: {data['bar']}")`).

* Start names internal to a module with a single underscore (`_foo`). Don't start names with double underscore (`__foo`); don't dunder (`__foo__`).

* End names with a single underscore only to avoid conflicts (`list_`).

* Define `__all__` when a file is a collection of functions.

* Use `assert` to check the internal consistency and verify the correct usage of methods, not to check for the occurrence of unexpected events. That is, the optimized bytecode should not waste time verifying the correct invocation of methods or running sanity checks.

* Complex compound statements (i.e., multiple statements on the same line) should be avoided. However, a second statement on the same line of a simple `if` can sometimes improve readability (`if value is None: return True`).

* Annotate all functions. Read the documentation of the module [`typing`](https://docs.python.org/3/library/typing.html#module-typing) for details; check [PEP-484](https://www.python.org/dev/peps/pep-0484/) and [PEP-526](https://www.python.org/dev/peps/pep-0526/) for additional information.

* Format source code using [Yapf](https://github.com/google/yapf)'s style `"{based_on_style: google, column_limit=120, blank_line_before_module_docstring=true}"`

* Follow [PEP-440](https://www.python.org/dev/peps/pep-0440/) for version identification.

### Classes

* Start names private or protected within a class with a single underscore (`_foo`); avoid name mangling if possible (`__foo`).

* Use nouns for properties, full sentences for methods (`foo.factors = bar.factorize(baz.formula)`).

* Do not implement getters and setters, use properties instead. Whether a function does not need parameters consider using a property (`foo.first_bar` instead of `foo.calculate_first_bar()`). Try not to hide complexity: if a task is computationally intensive, using a method might be wiser (`number.get_prime_factors()`). 

* Do not override `__repr__`.

* Explicitly derive container classes from `collections.abc`.

* Take advantage of the `abc` infrastructure when defining abstract classes (i.e., inherit from the helper class `ABC`; use the decorators `@abstractmethod` and `@abstractclassmethod`).

* Remember to override `__getstate__` and `__setstate__` if you define `__slots__`; write these functions in the very beginning of the class, before `__init__`. Define `__slots__` only if you are really confident about it.

### Comments

* Use English for names, in docstrings and in comments. Favor formal language over slang, wit over humor, and American English over British.

* Explain the purpose of all functions and classes in docstrings, docstring should give enough information to write the calls and use the classes; be verbose when needed, otherwise use single-line descriptions (note: each verbose description also includes a concise one as its first line).

* Be terse describing class methods, but verbose in the class docstring, possibly including usage examples. Be descriptive (`"""Calculates the next Mersenne prime."""`) rather than imperative. Comment public attributes and properties in the `Attributes` section of the class docstring (even though PyCharm is not supporting it, yet). Comment `__init__` only when its parameters are not obvious. 

* Do not explain basic class customizations (`__str__`, ...).  Use the formats suggested in the [Google's style guide](https://google.github.io/styleguide/pyguide.html&#35;383-functions-and-methods).

## Conventions

### Paranoid classes

`Paranoid` classes implement `run_paranoia_checks()`.

```python
class Paranoid():
    def run_paranoia_checks(self) -> bool:
        return True
```

The functions named `run_paranoia_checks` perform sanity checks. They always return `True`, but stop the execution throwing an exception as soon as an inconsistency is detected. The functions are not supposed to be called in production environments (i.e., when `-O` is used). Hint: it is safe to use `assert some_object.run_paranoia_checks()`. 

Paranoia checks should call the parent's check upon termination, that is, they should end with `return super().run_paranoia_checks()`.

### Pedantic classes

`Pedantic` classes implement `is_valid(obj)`.

```python
class Pedantic(ABC):
    @abstractmethod
    def is_valid(self, obj: Any) -> bool:
        raise NotImplementedError("Abstract method not implemented")
```

The functions named `is_valid` checks an object against a specification (e.g., an object against its semantic, an element inside a collection). They return either `True` or `False`. Hint: sometimes it could be useful to inlude them into `run_paranoia_checks`:

```python
def run_paranoia_checks(self):
    assert self.is_valid(self.value), "Meaningful message"
    return return super().run_paranoia_checks()
```
