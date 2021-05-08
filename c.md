# C

> **Notez Bien**: All these rules are meant to be broken, **BUT** you need a very good reason **AND** you must explain it in a comment.

## Style

### Names (TL;DR)

* `function_name`, `_static_function_name`, `MACRO_NAME`, `StructName`, `new_type_t`, `NEW_TYPE_ALT`, `GlobalVarName`, `_StaticGlobalVarName`, `local_var_name`, `t`, `function_param_name`.

### General

* Follow this order for the sections inside source files: **system includes**, **project-specific includes**, **struct and type definitions**, **prototypes**, **global variables with external linkage**, **global variables with internal linkage**, **functions**. Always use prototypes, functions order inside the file should be irrelevant.
* Don't start identifiers with a double underscore (`int __foo;`), don't shadows identifiers from the standard libraries (`int printf = 23;`). Don't rename the arguments of `main` (use `argc` and `argv`). Don't use single-character identifiers that could be misinterpreted on a printout (`l`, `O`).
* Use nouns for variables, full sentences for functions (`factors = factorize(formula);`); predicates (i.e., functions returning a boolean value) should start with the `is_` prefix (`if is_gargled(quz) { ... }`).
* Use long comprehensible names for global variables. Use long comprehensible names for local variables that may be meaningful in different part of the code; declare such variables in the beginning of the function, but initialize them the closest possible to their first usage. Use very short names for variables with limited semantic span; declare and initialize them in the smallest possible scope.

```c
int  last_useful_index;
// several lines...
last_useful_index = -1;
for(int t = 0; t < NUM_ELEMENT; ++t) {
    int u = complex_function(GlobalData[t]);
    another_complex_function(u);
    if(is_useful(u) {
        last_useful_index = t;
    }
}
``` 

* Declare structs in the beginning of the source file. If a struct is only useful as a local variable in a function, don't assign it any name. 
* Typedefs names can be either in all capitals (`BYTE`) or ending with a `_t` (`byte_t`), try to be consistent in each project. It is possible to `typedef struct _FOO { ... } FOO;` instead of `typedef struct { ... } FOO;` if `struct _FOO` is required.
* Declare multiple variables on the same line to stress that they are strongly related (`int pos_x, pos_y;`). Also consider using a struct in such cases.
* Keep the asterisk attached to the variable name when declaring a pointer (`FILE *foo;`).

* Use a [K&R style](https://en.wikipedia.org/wiki/Indentation_style#K&R_style) for indenting the code. Suggested: the *Linux kernel* variant with tabs replaced by 4 spaces.
