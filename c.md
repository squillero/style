# C

> **Notez Bien**: All these rules are meant to be broken, **BUT** you need a very good reason **AND** you must explain it in a comment.

## Style

### Names (TL;DR)

* `function_name`, `_static_function_name`, `MACRO_NAME`, `StructName`, `new_type_t`, `_STRUCT_TYPE_NAME`, `STRUCT_TYPE_NAME`, `GlobalVarName`, `_StaticGlobalVarName`, `local_var_name`, `t`, `function_param_name`.

### General

* Follow this order for the sections inside source files: **<system includes>**, **"custom includes"**, **structs**, **typedefs**, **prototypes**, **GlobalVariables**, **functions**. Always use prototypes, functions order inside the file should be irrelevant.
* Don't double underscore (`__`), don't shadows symbols from the standard libraries (`int printf = 23`). Don't rename the arguments of `main` (`argc` and `argv`).
* Use nouns for variables, full sentences for functions (`factors = factorize(formula)`); predicates (i.e., functions returning a boolean value) should start with the `is_` prefix (`if is_gargled(quz):`).
* Use very short names for variables with short life span; declare them in the smallest possible scope. Use long comprehensible names for local variables that are meaningful in different part of the code; declare them in the beginning of the function; initialize such variables in a line close to their actual usage, to ease cut n'paste.

```c
int  last_useful_index;
// several lines...
last_useful_index = -1;
for(int t = 0; t < NUM_ELEMENT; ++t) {
    if(is_useful(GlobalData[t]) {
        last_useful_index = t;
    }
}
``` 

* Typedefs names can be either in all capitals (`BYTE`) or ending with a `_t` (`byte_t`), try to be consistent in the project. It is possible to `typedef struct _FOO { ... } FOO;` as far `struct _FOO` is never used.
* Declare structs in the beginning of the source file. If a struct is only useful as a local variable in a function, don't give it any name. 
