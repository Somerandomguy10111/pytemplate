## Codebase rulebook

### I: Design by contract: Guaranteeing and assuming type hint conformity

Functions
- **Arguments**: All function arguments must be type hinted. 
     - Passing the correct type in arguments is **caller responsibility**
     - The Callee assumes that passed argument conforms to type hint
- **Returns**: All functions return an object that conforms to its type hint or raise an error. Note that returning and raising are mutually exclusive. 
    - Returning the correct type, assuming type conformity of the passed arguments, **is callee responsbility**:
    - The caller assumes that returned object, if any, conforms to its type hint
    - Functions without a type hint are implicitly assumed to return None

Classes
   - **Attributes**: All class attributes must be type hinted and conform to their type hints throughout their lifetime
     - The "__init__" method defines the attribute type in a single type hint outside of conditional statements
     - The "__init__" method must guarantee the integrity of the type hint upon return, assuming type conformity of arguments
     - All methods manipulating attributes must maintain the integrity of the "__init__" type hint, assuming type conformity of arguments
     - All methods retrieving attributes can assume the integrity of the type hints
   - **Inheritance**: Inherited attributes and methods implicitly inherit their type hints

### II: Naming

- Stick to pythonic case and spacing conventions (see also: [python-naming-convention](https://github.com/naming-convention/naming-convention-guides/tree/master/python):
  - source files: lowercase w/ snake_case, 
  - functions:  lowercase w/ snake_case; use verbs
  - classes: everything else: CamelCase; use nouns
- Function naming templates:
	- Functions that retrieve something that already exists `get_[object]` or `retrieve_[object]`
 	- Functions that create and then return an object `create_[object]` or`make_[object]`
- Names are searchable and distinguishable:
	- No shadowing of outer scope
	- Word trees are distinguished by prefix not suffix (e.g. plot_reference_fourier, plot_original_fourier instead of plot_fourier_reference, plot_fourier_original)
 	- Loop variable names contract the list variable name (e.g. instead of "for number in numbers:" use "for n in numbers:")
- Only use Hungarian notations when the object appears as several types throughout the program

### III: Vertical arrangement

- **Downward dependency rule**: Arrange modules so that dependency points downward. This is also referred to as the stepdown rule.
	- For functions: Top level function first, then functions called by top level function below. Proceed in the same manner at each level. If multiple functions are called, sort by call order
	- For modules/files: Consider l0, l1, etc. structure to establish downward dependency of modules within directories

### IV: Size rules

- **Minimal nesting**: Max indentation level === 3 
- **Small directories**: Each dir ideally contains only 2-4 files/folders; max 5 files/folders
- **Short files**: Max ~200 loc, Ideally < 120 loc
- **Short functions**: Max ~30 loc, ideally <= 15 loc; Ideally <= 2 args, max ~ 5 args
- **Commit messges**: ~ 5 words
  

### V: Misc

- **kwargs only**: Pass function arguments only by keyword
- **Comments require justification**: Comments should not be used to explain code where code can explain itself. Only use when you have justification such as:
	- Pointing out a temporary workaround e.g. to work around a bug in employed module
   	- Pointing to a relevant resource e.g. linking to API docs in a function that wraps the API
 	- Explaining unintuitive statements/commands; As often cited have the comment explain the why not the how
- **One repo, one env, one command**: Each repository should have only one environment that be launched in a single command. If you think that your repo needs several environments you instead need to split the repo.
