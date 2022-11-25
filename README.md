# Eons Language of Development

This repo describes the Eons Language of Development specification and provides interpreters where appropriate.

The goal of this language is to provide a concise but powerful means of describing data and operations at any scale. The same syntax for iterating over memory addresses in an embedded should be the same syntax for iterating over servers in a network. 

The Eons Language of Development is the emulsifier between the practical applications developed on the [Eons Python Library](https://github.com/eons-dev/lib_eons) and the powerful, but largely theoretical concepts created by the [Eons Develop Biology library](https://github.com/develop-biology/lib_bio). 

 The Develop Biology Library (aka Biology) provides the basics for creating a directed, recursive hypergraph. In short, this means data of any dimension ("hyper") flows ("directed") through a network ("graph") of connected nodes, where each connection and node may be graphs unto themselves ("recursive").

 The Eons Python Framework extends this directed, recursive hypergraph by simplifying the numerous classes in Biology into a single Functor and wrapping the complexities of Biology's myriad context frameworks into a single system of [Implicit Inheritance](https://github.com/eons-dev/lib_eons#implicit-inheritance).

Through the combination of these frameworks, we can blur the lines of what it means 'to be', 'to have', and 'to do': Biologically Bonding Atoms makes it so that "having" relationships defines who you are (the same way a molecule is defined by its constituent atoms), and when everything is a Functor, what you are determines what you do and vice versa.

From this abstract vantage point, we may rethink what it means for a language to be 'functional' vs 'object oriented' and much more. We will now turn our focus to the language we have developed to wrap our complex theories into something practical: Eons Language of Development.

## Interpreters
Coming soon!  
This language will have several interpreters, the most important of which will be defined here as a `bio::chemical::Axis` for use with Eons Develop Biology.

## Case Insensitivity
The EONS LANGUAGE OF DEVELOPMENT is case insensitive. `myVarIablE` is the same as `myvariable`.

We recommend snake_case for all variable and function names.

## Blocks
Eons Language of Development is almost like an object-oriented lisp variant and relies heavily on the meaning of different braces instead of keywords.

The Blocks used are:
* `##` - Comment: used for docs & non-evaluated sections of code.
* `''` - String: used for strings.
* `[]` - Container: used to manage repeated elements.
* `{}` - Execution: used to define and evaluate functions.
* `()` - Parameter: used to define and bind Surfaces.
* `<>` - Type: used for inheritance and meta programming.

These Block structures are strictly enforced to enable consistency (i.e. there are no other supported Comment Blocks, etc.)

Each Block is allowed to change how symbols are interpreted within it. For example, the Comment Block does not execute code, and adding "{}" inside a string does not define an Execution Block

String and Comment Blocks (`''`, `##`) are considered "non-coding" while all other Blocks are considered "coding".
Type and Execution Blocks are considered "instantiating" while Parameter and Container Blocks are considered "describing"

### Block Precedence
Blocks are interpreted in the following order:
1. `''` String Blocks are processed first.
2. `##` Comment Blocks precede all coding blocks.
3. `[]` Container Blocks are the first coding Block to be processed, allowing them the most dramatic code changes.
4. `{}` Execution Blocks must be processed before Type Blocks.
5. `()` Parameters are processed after Execution.
6. `<>` Type Blocks are processed last to allow alternative interpretations of `<` and `>`.

### The Need for Containers
Containers are the Eons way of cramming multiple values into a single symbol. We don't support `*args` or numerous variations on the set. All we provide is a "many" notation.

To expand a container, you can use an empty `[]` after the container symbol.
For example:
```
my_container = ["a", "b", "c"]
my_container[] # expands to "a", "b", "c" #
```

## Types
There is only one type in the Eons Language of Development: the Functor (Protein in Biology).

All data structures, functions, etc. can be mutated into each other.

Types are written as `my_object<my_type>`.
For example:
```
animal<>
(
    legs <int>
    color <> # <- empty type is okay #
)
cow <animal>
{ # <- note the use of the Execution Block, rather than the Parameter Block #
    legs = 4
}
```

There are no differences between arrays / lists, maps / dictionaries, sets, etc. In Eons Language of Development, items in a Container may be mixed and match to your liking. If you would like to enforce type checking, create a specialized Functor which defines your addition Operators (e.g. `+` and `+=`).

If you do not know the type you want ahead of time, just leave the `<>` empty. You can always add and change types later.

### Return Types
Functors (Proteins) can take multiple inputs and give multiple outputs. Because of this, there is no "return value", as there is in typical functions. Instead, the members of the Functor may be accessed after it has been executed.

You'll see plenty of examples of this throughout this spec.

## Operators
The Eons Language of Development does not use any keywords; all information necessary to interpret code is presented as Operators. This means that any words are user defined and not part of the built in language.

The Operators used are:
* `,`, `;`, `\n` (newline) - End.
* `.` - Access, also referred to as spatial separation.
* `\` - Exit & Sequence, also referred to as temporal separation.
* `?` - Condition
* `&` - And
* `|` - Or

The space is a dynamic Operator that is filled in depending on the context of where it is found. See the [Spacing Autofill rules](#spacing-autofill), below.

Besides those for Blocks, these are the only characters used by the Eons Language of Development. All other symbols (e.g. `+`, `-`, `*`, `/`, `%`, etc.) are all user defined and can be changed as thou wilt.

You may also override `<` and `>` for comparisons (and thus `<=`, `>=`, etc.). See [Declaration and Evaluation](#declaration-and-evaluation), below, for more info.

### Exiting and Returns
The Exit Operator exits the current Execution Block, whatever that may be.

`\var` returns `var`, exiting the current Execution Block.
To exit without returning anything, simply `\;` (or use any appropriate line ending).

You can also type `return` in place of `\`. Though be aware that `return` can be overridden (e.g. maybe you want to log all values provided by all Functors).

### Escaping
Still use `\` to escape other characters.

**You should only ever need to escape characters within a string** (e.g. `my_\n_var` is not a valid variable name). Because String Blocks are non-coding, this is fine. Within a string, `\` will not be interpreted as a Sequence, so we maintain it as the escape character.

### Line Endings and Code Separation
Code may be separated by any End Operator. All are equally valid in all contexts.
End Operators are not necessary where a Block terminator is present. For example, `[my,list]` does not need to be `[my,list,]` because the `]` separates the code from whatever may follow.

### Access and Spatial Separation
`this` is the keyword for the current scope.

The access Operator (`.`) is used in increasing order of scope, similar to how domain names are `subdomain.domain.top-level-domain`.
This ordering is reversed, as compared to most other programming languages, but should be familiar, as it's how we all handle URLs and file extensions. The benefit of this order is that you only need to append what is absolutely necessary and the most important scope is immediately apparent, when read from left to right.

In the Eons Language of Development, this increase in scope allows us to easily access variables defined in encapsulating spaces (Vesicles or Solvents, in Biology).
For example:
```
my_class<>
(
    constructor(name<string>)
    {
        #
        'this' comes after name to indicate the greater context to which 'name' belongs
        it is also necessary to specify 'name.this', since the local context overrides the parameter.
        #
        name.this = name
    }
    
    say_hi()
    {
        #
        here, there is no other context to which 'name' could belong beside 'this', so no additional specification is necessary.
        however, additional specificity does not hurt.
        #
        print name
    }
)
```

Spatial separation also applies to competing parent scopes. Say you have a class which 'inherits' from `parent1` and `parent2`. If both parents define `some_var`, you can access each parent's value with `some_var.parent1` and `some_var.parent2`, respectively. If no greater domain is suffixed to `some_var`, it would be an error. However, if you define `some_var` in your class and then use the variable without a suffix, it will default to `some_var.this`, since `this` is the 'closest', 'spatial' scope to where the variable is used.

#### TODO: Implicit Spatial Scopes
Eons Python Library allows you to specify the precedence of spatial scopes with Fetch. That behavior needs to be ported to Biology.

### Sequences, Synapses, and Temporal Separation
Sequences enable tasks to be accomplished dynamically: the same set of instructions can yield two different results when executed in different orders. Sequences are created using the Sequence Operator (`\`). They implicitly execute each step along their path and make the previous Steps methods and members available to the subsequent Steps. **Only the last step in a sequence is returned.** Please note that, as with all executions, the **whole** Step object is returned so that any part of it may be accessed.

The Eons Python Library calls this system of Sequences ["Implicit Inheritance"](https://github.com/eons-dev/lib_eons#implicit-inheritance).

For example, `find\my\scarf` calls the `find` Functor's Execution Block, then makes all methods and members in `find` available to `my`, then call's `my`'s Execution Block, then makes all methods and members in `my` available to `scarf`, then **returns** `scarf`'s Execution Block. You can then build a `your` Functor and call `find\your\scarf(color=blue)`; or create a `store` Functor for `store(in=["garage","attic")\my\things`, etc. The point in adding Sequence support to the language is to encourage reusable code. If you can make your Functor sequence compatible, it can be (ab)used in many marvelous ways!

You can use Sequences anywhere you could evaluate an expression (they are one and the same).

Note that Sequences read left to right as they build upon each other: `first\second\third`.

#### Returning a Sequence
If you prepend a Sequence with the Exit Operator (e.g. `\find\my\scarf`), the Sequence will be evaluated and the last Step will be returned from the current Execution Block.

### Merging Spacetime
You can create spatial constructs using temporal sequences by wrapping them in a type block. Because the whole Functor from the final step in a sequence is returned and that Functor contains the members and methods of what came before it, you can simply set this functor as the parent of the object you're creating. When called from a Type Block, a Sequence will only merge the Execution Blocks of each Step, it will not execute them. 

For example, `scarf_finder <find\my\scarf>` allows you to later call `scarf_finder()` to execute all steps at once. Note that you can also set defaults here; `scarf_finder <find\my\scarf(color=blue)>` is roughly the same as `scarf_finder <find\my\scarf>(color=blue)` and can be overridden when calling `scarf_finder(color=red)`.

### Parallel Sequences
It is possible to execute multiple Sequences in parallel. To do this, simply use a Container.

For example, `find\[my,your]\scarf` would execute `find\my\scarf` and `find\your\scarf`. This would return both the modified `scarf` objects in a Container: `[find\my\scarf, find\your\scarf]`.

If the Functors you execute are configured to run in different threads, these jobs will be executed in parallel.

You can also achieve this same functionality by defining the asynchronous behavior in the execution block of your Functor. For example:
```
custom_async(to_execute)
{
    custom_thread_engine\to_execute[]
}
find\custom_async([my,your])\scarf
```

## Declaration
Symbols are defined when either the Type Block (`<>`) or Execution Block are used.

You cannot change the `<>` nor `{}` without redefining the symbol!

This means `my_class()` will execute the `my_class` symbol defined elsewhere. Whereas, `my_class<>()` is a declaration and will not execute any code. The same is true for `my_function()` vs `my_function(){}`. Note as well that `my_class(){}` and `my_function<>()` are valid declarations (you can use this when combining functions, e.g. `combined_function<do_first, do_second>(extra_arg<>)`).

However, both `<` and `>` may be used in evaluated expressions as comparisons. The difference between the Type Block and the less than & greater than symbols is that the latter are always followed by `?`, `&`, or `|`. 

**It if forbidden to declare or change types in a comparison statement**. That's how we solve that problem.

## Execution
If an expression lacks `<>` or `{}`, it will be executed (e.g. `function_call()` or `function_call` vs `function_declaration(){}`).
All executed statements (i.e. those within a `{}`) must be separated by a valid line ending (`,`, `;`, or `\n`).

Redefining a symbol changes the existing symbol for all future execution. Meaning, `symbol symbol{do_this_instead}` will change the behavior of `symbol`. However, `symbol symbol`, without a Type nor Execution Block will be executed per the Spacing Autofill rules below.

### Spacing Autofill
These rules apply to any set of symbols separated by spaces:
* The last symbol is always wrapped by a `()` for the previous symbol.
* If there is only one symbol, it is as if an empty `()` is appended to the end of it.
* If there are many symbols separated by spaces, for all but the last, the order is inverted and they are joined by `.`s.

This means we can define `+` as a custom function in an object and say `a + b`, which becomes `+.a(b)`. We can also do `a unary add something.b`, which becomes `add.unary.a(something.b)`. Note that `a + b` is NOT the same as `a+b`; the latter is a single symbol, e.g. `a+b<parent_class>(arg<>){do_stuff}`.

## Type Casting
A type may be treated as another type if it defines the target type as a member variable.

Type casting happens implicitly whenever a function argument is declared to have a type.
Type casting happens explicitly whenever the type member is accessed.

For example:
```
inventory_number<>
(
    tracking_id<int>
    
    # Make inventory_number castable to an int #
    int<traking_id>
    
    #
    The above could also be written as:
    int{\tracking_id}
    or 
    int{return tracking_id}
    #
)

ship(number<int>)
{
    ...
}

some_item<inventory_number>

ship some_item
#
This line calls ship(int.some_item), which returns the tracking_id from the inventory_number parent
#
```

## Control Flow
There are 3 forms of control flow available in Eons Language of Development: 
* `if` & `if else` statements
* `foreach` loop
* `while` loop

The `if` statement is defined as `...?{}` and the `if else` statement is defined as `...?{}{}`, where `...` is the condition to check.
Note that the `?` will always cast the preceding statement to `bool`. It is an error if `bool.my_type` returns an `int`, etc.

The `while` loop is defined as `(...){}`, where `...` is the condition to run the loop again. Like `if` statements, `while` loops will cast their condition to `bool`.
To exit a while loop, use the Exit Operator (`\`). You may also return a value from a `while` loop with `\var_to_return`. You may also type `break` in place of `\` but be aware that the behavior of `break` can be overridden.

The `foreach` loop is defined as `container[iterator]{action}`, where `container` is the Container to iterate over (previously defined by `[some, set]`) and  `iterator` is the symbol to use within `action` to represent the current item in the `container`. To enable type checking in a foreach loop, simply specify a Type Block after the iterator name.
For example,
```
my_list = ["a","b","c", 1, 2, 3]

# Foreach loop, using [iterator<type>]{...} #
my_list[letter<string>]
{
    print letter
}
```
would likely print "abc" (depending on the implementation of `print` and assuming `string` hasn't been hacked to identify numbers, etc.)

## Container Comprehension
A Container can be expanded into its constituents by appending `[]`. You can further restrict this behavior by specifying a Type Block and / or a Parameter Block within the Container Block.
For example,
```
color<>
(
    name <>
)
dog<>
(
    name <string>
)

my_colors_and_dogs = [color(name='red'), color(anme='blue'), '#00FF00', dog(name='red')]

my_colors_and_dogs[<color>] # gives [color(name='red'), color(name='blue')] #
my_colors_and_dogs[(name='red')] # gives [color(name='red'), dog(name='red')] #
my_colors_and_dogs[<dog>(name='red')] # gives [dog(name='red')] #
```



These rules are applied depending on the number of symbols separated
* If there is no RHS, an empty `()` is appended to the end of the function call (e.g. `func;` becomes `func();`)
* If there are multiple symbols se
* If LHS is a Protein and RHS is a Vesicle or Cellular Structure, a wrapping `()` is applied to the RHS.
* If LHS is a Protein and RHS is also a Protein which is defined as a Surface on the LHS, a `.` is added to replace the whitespace between the symbols.
* If LHS is a Protein and RHS is also a Protein which takes at least 1 argument and is not defined on the Surface of the LHS, the LHS will be type-casted to the type of the first argument of RHS (e.g. `add(1,2) > 3` becomes `add(1,2).int.>(3)`). This may result in an error if the type-cast fails or if the type-casted LHS does not implement RHS on its Surface.
* It is an error if LHS is a Protein and RHS is also a Protein which takes no arguments and is not defined on the Surface of the LHS.
* If the LHS is a Vesicle or Cellular Structure and the RHS is a Protein, Vesicle, or Cellular Structure, a `.` is added to replace the whitespace between the symbols.

Thus, consecutive symbols become expressions in a right to left manner to automatically fill in function calls and member access. 

 It is an error if the LHS is a Vesicle or Cellular Structure and does not define the given symbol or if the LHS is a Protein which does not have a Surface of the RHS type and the RHS cannot be converted to a type the LHS takes (see below for more on type conversion).

You cannot declare variables in an execution Block (`{}`).  
You may execute expressions in declaration Blocks (`()` and `[]`) and type Blocks (`<>`), provided that they:
* include single-Block expressions (i.e. `functionCalls()` or `indexAccess[]`) and
* do not contain spaces (i.e. none of the `symbol symbol` autofill logic is enabled in declaration Blocks).

Members defined within an object's `[]` will only be searched within that object's `{}`. No other object within or without shall have access to an object's Internal members. The only exception to this is Transcription Factors, which have access to any `[]` they can reach.

It is an error if a member is declared in both a `()` and `[]`. The same symbol can be used in a `<>` as in either `()` or `[]`, since the meaning of `<>` is dependent on the object to which it applies and will never be used for member definition.

Surfaces may be accessed by their name or simply by their index using the `[]` Operator in an executable expression. Index Operators take either a numeric position (e.g. `[0]`) or a string corresponding to a Surface or Internal member name (e.g. `['myVar']`).

Any symbols which begin with `__` (2 underscores) are compiler defined and may not be changed. It is illegal for your variables to begin with underscores.

Proteins (i.e. functions, or more accurately functors, or even more accurately `()[]{}`) do not have return types. This is to enable multiple and delayed access to returned values.
If you would like to treat a Protein as a type, you may define a type conversion for the Protein, which will make the syntax appear as a return value in other languages. There's more on that below.

Neurons, specialized Cellular Structures, may be connected via `<>()[]{} --- <>[]{}{} ---> <>()[]{}`, `<>()[]{} <--- <>[]{}{} --- <>()[]{}`, or `<>()[]{} <--- <>[]{}{} ---> <>()[]{}`. Meaning that in a `source --- Synapse ---> target` expression,  a `source` Cellular Structure is connected to a `target` Cellular Structure through a `Synapse`. See Examples below for more info. 


## What Gets Run
When running a .bio executable, all standalone execution Blocks are combined in the order they are found into one `main(){}` function.

If multiple execution Blocks have the same name, only the last is taken in the position in which it is found.

For example:
```
//possibly from including an external library
main()
{
    print('this Block is shadowed by the main(){} later on');
}

...

setup()
{
    print('setup');
}

...

main()
{
    print('main');
}
```
would output:
```
setup
main
```

Note that all variables must be declared within the executable's Surface and cannot be declared within the execution Block.

Let's create an `example.bio` executable with the contents:
```
main
(
    toPrint int = 5;
)
{
    //toPrint int = 5; // <--- INVALID. Variables cannot be declared within a {}
    print(toPrint);
}
```
This allows the program to take arguments: `./example.bio --toPrint=10` would output '10'.

When multiple executables have Surfaces, the Surfaces are combined in the order they appear.

Let's make `example2.bio`:
```
first
(
    name string
)
{
    print('Name: ' + name);
}

second
(
    id int
)
{
    print('Id:' + id);
}
```
which is condensed to:
```
__main
(
    name string,
    id int
)
{
    print('Name: ' + name);
    print('Id:' + id);
}
```
We can then say `./example2.bio myName 5`, which would output:
```
Name: myName
Id: 5
```

## Copy by Reference by Default
Objects are normally copied by reference and any change to the object will be changed in all locations.
These changes are thread-safe by default and may wait on other threads.

However, if you would like to copy an object by value (possibly for non-Blocking or destructive access to the object), indicate such in the type declaration.
For example:
```
add(first int*, second int*, result int)[]
{
    result = first + second;
}
```
Here, `first` and `second` are copied by value and will remain a part of the `add` Protein until they are unbound.

## Garbage Collection
When an object has no references, it is deleted. This is handled through the `chemical::` `solution` system in the underlying C++.

## Function Arguments
Arguments may be provided by order or by symbol specification. For example, consider:
```
add(first int, second int, result int)[]{result = first + second;},

main
(
    three int
)
{
    three = add(1, 2).result;
    three = add(1, second = 2);
    add(1, 2, three);
    add(1, 2, result = three);
}
```
All of these are valid ways to use the `add` Protein.

Note that we can treat `add` as if it had a return value with:
```
add
(
    first int,
    second int,
    result int,
    
    //'return value' See the section on Type Conversion, below, for more info.
    int result
)
[]
{
    result = first + second;
}
```
Now, we can say `three int = add(1, 2)`, without needing to specify `.result`.

Here's another example:
```
sort(array <>())
[
    index int,
    buffer * //we want buffer to be any type, so we mark it as '*', which allows us to set the type and value later with '='.
]
{
    array size <= 1 ? {break};
    
    //the above statement is dense.
    //array size expands to array.size(), which gives the number of Surfaces in a Vesicle or Cellular Structure (and may be overriden).
    //the rest of the if condition expands to: array.size().<=(int).
    //the Eons Language of Development interpreter will check array.size() for an int conversion, which exists, and thus will call: array.size().int.<=(int).
    //the if statement then reads ...int.<=(int).bool 
    //the if statement (i.e. condition ? {true case};) does not require the word 'if' nor parenthasese and is terminated with a ';', just like every other expression.
    //because 'break' is the last (and only) expression in the if execution Block, it does not need to end with a ';'.
    //'break' ends the function, returning control to the caller.
    
    index = 0;
    (true) //while loop
    {
        //index + 1 must have spaces and expands to index.+(1)
        //The following becomes: array[index].>(array[index.+(1)]).bool ? ...
        
        array[index] > array[index + 1] ?
        {
            buffer = array[index];
            array[index] = array[index + 1]; 
            array[index + 1] = buffer;        
        };
        
        index ++; // note the space after 'index', making the expression expand to index.++().
        index == array size - 1 ? {break}; 
    };
}

Pair <>
(
    name string,
    value int,
    
    int value //Type Conversions (for predefined '>' operation)
)

main
(
    heterogeneosuMap <>
    (
        var1 Pair = ('One', 1),
        var3 Pair = ('Three', 3),
        var4 int = 4,
        var2 Pair = ('Two', 2)
    )
)
{
    sort(heterogeneosuMap);
}
```
This will result in `heterogeneosuMap` being rearranged as:
```
heterogeneosuMap <>
(
    var1 Pair = ('One', 1),
    var2 Pair = ('Two', 2)
    var3 Pair = ('Three', 3),
    var4 int = 4,
)
```
This works on `heterogeneosuMap` with a mixture of Pairs and int(s) just as it would on any data which can be represented as an array of ints. Note that the int requirement only exists because of the `int.>(int)` call, which only takes ints. If we had a map consisting of custom types which implemented `> (other CustomType)[]{}`, this would work just as well.

## File Inclusion

`&'/path/to/file.bio'` will include all the contents of the specified file in the exact location the `&` statement occurs in.

This means you can do crazy things like create a file with the contents:  
`'FunctionDefinition.bio'`
```
doStuff(with, internals)
```
And then use that file in your code:
`'Main.bio'`
```
MyFunction(with int)[internals <>()]
{
    &'FunctionDefinitions.bio'
}
```

## Symbol Resolution

### Execution Blocks
When an execution Block looks up a symbol, it begins with the Internal members of the object it is operating within, if there are any. Next, the Surfaces of the object (if there are any) are checked. If a symbol is not found within the `[]` or `()` of an object, the Surfaces of the containing executing object, if one exists, are searched recursively until a match is found. If no match is found within the declared variables leading to the currently executing expression, the global context is searched as read-only. Write operations on globally declared objects are forbidden.

This has 2 important implications:
1. Variables may be context defined and, unlike other languages, do not always need to be explicitly supplied to the currently executing context.
2. Symbols defined closer to the point of execution take precedence over those defined farther away.

To illustrate the first point, consider the function:
```
addImplementation()[]
{
    result = first + second;
}
```
This code is valid only in a context like this:
```
add
(
    first int = 1,
    second int = 2
    result int
)
[
    //NOTE: none of first, second, nor result can be Internal as 
    //  Internal symbols are only accessible from the matching execution Block, 
    //  not the sub-execution Blocks contained within.
]
{
    addImplementation
}
```
Here, `addImplementation` sets the value of the `add` Protein's `result` using its `first` and `second` surfaces.

This makes it possible to 'pass' the caller transparently to other execution Blocks, the same way `this` is passed transparently to C++ methods.

Note that there is no way to access a callers methods by number. You cannot say `[0] + [1]`, as this notation explicitly references the Surfaces of the current object and will never reference the Surfaces of a greater context. If you would like access to the Surfaces of the caller without referencing them by name, you must have the caller pass the relevant symbols to the current object's Surfaces.
For example:
```
addImplementation
(
    toAdd *
)
[]
{
    result = toAdd[0] + toAdd[1];
}
add
(
    values <>(int)
    result int
)
[]
{
    addImplementation values
}
```

To illustrate the second point, consider what would happen if `addImplementation` defined `result`:
```
addImplementation
(
    toAdd *,
    result int // <--- result will no longer affect the caller's member.
)
[]
{
    result = toAdd[0] + toAdd[1];
}
```
By moving the `result` variable closer to its use in `addImplementation`, we more rigorously define what `addImplementation` can do and thus must treat it differently. `add` must become:
```
add
(
    values <>()
    result int
)
[]
{
    result = addImplementation(values).result
}
```

### Function Arguments
Symbol resolution is more strict in function arguments, i.e. `(name = value)`. Here, `name` must exist on the object's Surface.

### Type Blocks
In Type Blocks `<>`, the names used must be valid, predefined objects of the single expected type. 
For all objects besides Plasmids, the expected type is a Transcription Factor. For Plasmids, the expected type is another Plasmid.

When declaring both Plasmids and Transcription Factors, the Type Block specifies the object's dependencies but has no direct effect on the object. When a dependency is declared in a Plasmid, it only signifies that some of the Transcription Factors the Plasmid defines are dependent on those from the specified Plasmid. When a dependency is declared in a Transcription Factor, not only does the dependency have to be declared first, the dependency's execution Block is copied into the top of the dependent Transcription Factor's.

Because symbols may only be redefined within a more specific context, global declarations of Plasmids and Transcription Factors will always generate errors if a Symbol is duplicated. This is preferred.


## Simple Neuron Example
An example of a Neuron could be:
```
MyNeuron /*A Neuron with gain control*/ <neuron>
(input int, output int) [gain int = 1]
{
    output = gain * input;
}
```
Here, we start the definition of `MyNeuron` with a comment Block (`/**/`). This acts as the documentation for the object. Note that newline characters are only ever interpreted in strings and comment Blocks, so you can have whatever fancy documentation you'd like. Other than strings and comments, newlines and all other whitespace is mostly irrelevant (more on that later). This allows us to put spaces and even newlines in our Blocks.  
Next, we specify the `neuron` Transcription Factor (TF). This tf will make what would otherwise be a `Cell` (`symbol<>()[]{}`) into a `Neuron` with the ability to receive and send signals.   
We then add 2 publicly accessible members, `input int` and `output int`. These are built-in `int` types but could be whatever we want. After defining our publicly available Surfaces, we define a private member `gain int` and set the default value to 1. Because `gain` is in square brackets (`[]`), it will not be accessible anywhere outside the execution Block (`{}`) of our `MyNeuron`, except in rare cases (such as with TFs, more on that later).  
Lastly, we define the execution Block on a new line and with indents. However, the indentation and white space do not matter. Notice the line ending used in the execution Block: `;`. These line endings are only needed to separate executed expressions from each other and are unnecessary when defining symbols, hence no line ending after we complete our `MyNeuron` definition.

## Simple Synapse Example
Now, let's create a Synapse to connect to our Neuron:
```
MySynapse <synapse>
/**
 * This synapse moves the outputs of one MyNeuron into the inputs of another. 
 */
[
    passthrough int
]
{
    //upstream is a magic value that is provided in the first execution Block of a Synapse.
    passthrough = upstream.output;
}
{
    //downstream is a similar magic value provided in the last execution Block.
    downstream.input = passthrough;
}
```
We've done a few things differently here. Notice that we changed the position of the comment Block to be after the TFs. This is valid; Blocks may appear in any order. The caveat to that is that Synapses have duplicated Blocks and the first one to appear is always provided the `upstream` value containing the source Neuron while the last is always provided the `downstream` value containing the target neuron.

Notice also that we use the `.` for member access and that we are accessing Surfaces of the provided variables. All variables are passed by reference and the `.` is the only member access specifier.

We can now use this Synapse with our connection notation: `SourceNeuron --- Synapse ---> TargetNeuron`.
Here's how that could look:
```
source MyNeuron --- MySynapse ---> target MyNeuron
```
Alternatively, we can declare our variables ahead of time:
```
main
(
    source MyNeuron,
    target MyNeuron,
    synapse MySynapse
)
{
    synapse --- SomeOtherSynapse ---> source
    source --- synapse ---> target
    source --- synapse2 ---> target
    source --- synapse3 ---> target
}
```
Alternatively, if we wanted to define our Synapse only using TFs, we could:
```
main
(
    source MyNeuron,
    target MyNeuron
)
{
    source ---
        []{}{}
        <
            all,
            of,
            these,
            //but,
            //not these
            transcription,
            factors
        >
    ---> target
}
```
Here, the Synapse declaration is a Type Expression.

## Asynchronous Cellular Structures and Event Dispatch
Most execution Blocks, such as Proteins, Transcription Factors, and Plasmids run synchronously and immediately in the thread in which they are called.

All Cellular Structures (i.e. `<>()[]{}`) execute their `{}` on a clock. The speed of their oscillation may be set with the built-in value `interval` in milliseconds (e.g. `MyCell<>()[]{interval ++;}`, which would make `MyCell` call its `{}` 1ms slower every time it's called). Cellular Structures do not always run in separate threads. It may be useful to have a Cellular Structure, like a tissue, contain other Cellular Structures and have their oscillations run in a single thread. Other times you may want maximum parallelism which can be accomplished by calling the built-in `fork()` function. All `fork()` does is move the Cellular Structure to a new thread. Note that you can just say `MyCell fork;`, which will expand to `MyCell.fork();`

Synapses are used to send data between asynchronous Cellular Structures. When a Neuron Fires (e.g. `MyNeuron exciteTrigger` is true), all `outgoingSynapses` execute their `upstream` Blocks in the calling thread, then execute their `downstream` Blocks in the thread they connect to. Synapses may store data Internally inorder to modify the signal sent including changing whether or not the signal is transmitted to the target at all. A Neuron firing event causes Synapses process all `upstream` execution Blocks first, then all `downstream` execution Blocks.

The `--- Synapse --->` (and thus `<--- Synapse --->` and `<--- Synapse ---`) method, which adds an outgoing connection from the source and an incoming connection to the target may be overridden with the following methods:
```
MyCustomClass
<>
(
    //Override outgoing functionality for all Synapses
    --- (outgoing <>[]{}{})[]
    {
        //YOUR CODE HERE
    }
    
    //Override incoming functionality for all Synapses
    <--- (incoming <>[]{}{})[]
    {
        //YOUR CODE HERE
    }
)
[]
{}
```

This allows you to define custom overrides for your specific types as well:
```
MySynapse <>
[
    //by defining members, we change the shape of the type, making it possible to target only the classes we want.
    custom string
]
{
    //...
}
{
    //...
}

MyOtherNeuron
<>
(
    //Override outgoing functionality only for MySynapse
    --- (outgoing MySynapse)[]
    {
        //YOUR CODE HERE
    }
    
    //Override incoming functionality only for MySynapse
    <--- (incoming MySynapse)[]
    {
        //YOUR CODE HERE
    }
)
[]
{}
```

### Rounding Error Protection
When a value is accessed by a Synapse through `upstream` or `downstream`, the value is marked as a Neurotransmitter and will be Reset() by the Biology framework every time the number of Synapses affecting the value drops to 0.

## Type Expressions
Type Expressions can be substituted for full types the same way defined symbols can be treated as types.
Saying `var MyNeuron` is just as valid as saying `var <neuron>(input int, output int) [gain int = 1]{output = gain * input;}`. These expressions are in fact identical. The only time you need to explicitly define the symbol name is if you are going to use it later.
Consider the above example:
```
source MyNeuron --- MySynapse ---> target MyNeuron
```
Since we have no need to modify `MySynapse` after we create it, we do not have to give the `MySynapse` type a name.

When declaring a type for the purposes of type-matching, the `<>`, `[]`, and `()` Blocks may be left empty, as they are not needed to check if an object has the necessary Surfaces. Thus the following is valid:
```
doSomethingWith(myNeuron (input int, output int)<>[]{})
[]
{
    myNeuron.input = 5;
}

main(myNeuron MyNeuron)
{
    doSomethingWith(myNeuron);
}
```
Even though `MyNeuron` is `<neuron> (input int, output int) [gain int = 1] {output = gain * input;}`, it can be used anywhere `(input int, output int)<>[]{}` can. It doesn't matter if the `neuron` Transcription Factor adds or changes members, as long as the type used with `doSomethingWith` is `()<>[]{}` and defines the `input int` and `output int` Surfaces, it's valid.

Aside: All types must have names.

### Type Perturbation
Type Expressions may be modified ad nauseam using the `&...` syntax where `...` is any Block besides strings (`&''` is only used for file inclusion). You are also allowed to join types together by symbol.

For example, we can define an `InputNeuron` and an `OutputNeuron` which combine to form `MyNeuron`. Using Type Perturbation, we can do this without Transcription Factors:
```
InputNeuron <neuron>
/*
    A Neuron with an input
*/
(
    input int
)
[]
{}

OutputNeuron <neuron>
/*
    A Neuron with an output
*/
(
    output int
)
[]
{}

MyNeuron InputNeuron &OutputNeuron &
/*
    A Neuron with gain control
*/
//NOTE: No () Block even though MyNeuron is a <>()[]{}
[
    gain int = 1
]
{
    //output from OutputNeuron.
    output = gain * input;
}
```

How the Type Perturbation mechanic works is by combining the contents of duplicate Blocks on a first-in first-out bases and then removing duplicates from the end.

Our `MyNeuron` thus has an intermediate state similar to the following:
```
MyNeuron 
<
    neuron, //from InputNeuron
    neuron //from OutputNeuron; this one will be removed.
>
/*
    A Neuron with an input
    A Neuron with an output
    A Neuron with gain control
*/
(
    input int,
    output int
)
[
    gain int = 1
]
{
    //output from OutputNeuron.
    output = gain * input;
}
```

This is useful when you want to build onto a type that was previously defined elsewhere without using Transcription Factors.

Type Perturbations do not afford any changing of variables; you will necessarily need to use Transcription Factors for that.

Additionally, Type Perturbations get more confusing when duplicate Blocks exist in the type definition, such as with Synapses (`<>[]{}{}`). In order to add to the second `{}`, you must provide 2 `{}` Blocks: `PerturbedSynapse MySynapse &{}{/*added to downstream Block*/}` vs `PerturbedSynapse MySynapse &{/*only added to upstream Block*/}`.

Type Perturbation only moves in one direction: toward complexity. You cannot directly simplify objects by Perturbing them (but you can indirectly by adding on a Transcription Factor which simplifies the object).

## Meta Programming and Inheritance
There is no inheritance in Eons Language of Development. This might be surprising considering how much inheritance is (ab)used in the C++ code underpinning the language. We believe it is cleaner and less error-prone to use simple meta-programming along with native code rearrangement through self-reflection.

Transcription Factors may perform arbitrary changes to the data structures they are applied to.
For example:
```
symbol <dependencies> 
{
    object.newSurface string;
    object.[].newVar int;
    object.existingSurface.[].internalValue = 4;
    object.{} += someExecutionStatement(newVar, newSurface);
    object.{}.someOtherFunction = (same type, of args)[but with, also these]{and(same, but, also, 'modified functionality');};
}
```
TFs use the same kind of magic variables that Synapse uses: our `object` here is provided to a TF so that it may affect whatever it is applied to.
TFs have access to all parts of all objects which may be reached through this provided `object`. This is accomplished through the `genetic::` `Localization` and `Insertion` mechanics.
In this example, `object.newSurface string;` creates a new `Surface` (i.e. `()`) called `newSurface` which is of type `string`. We don't need to specify `object.().newSurface`, as we do with the Internal (i.e. `[]`) variable `newVar`. This is because members are exposed (i.e. public) by default and by specifying `object.[]`  only when making members Internal (i.e. private), we save ourselves some work.
`object.existingSurface.[].internalValue = 4;` shows how TFs have the ability to modify ANY Internal value they can access, not just those of `object`.
The line `object.{} += someExecutionStatement(newVar, newSurface);` appends a new execution statement to whatever object already had in its execution Block (i.e. `{}`).
The last line of this example uses the syntax `object.{}.someOtherFunction ...` which addresses all instances of `someOtherFunction` within the object's execution Block. This does not affect `someOtherFunction` in any other object.

You are also allowed to modify comments and strings through these same mechanics. `object./**/ += 'New documentation';` is valid.

You may remove a line-item from an object using the built-in `__remove()` method.
For expample:
* `object.__remove(symbol)`
* `object.[].__remove(symbol)`
* `object.{}.__remove(expression)`
* `object.subobject.[].__remove(symbol)`

### Composition
The easiest way to reuse the code you've written is through composition. Let's take the `someOtherFunction` example from above and assume you wrote:
```
MyModifiedFunction
(
    same type,
    of args
)
[
    but with,
    also these
]
{
    and(same, but, also, 'modified functionality');
}
```
You could then create a TF wrapper to enable code reuse with the following:
```
modifyFunctionality <>
{
    object.{}.someOtherFunction = MyModifiedFunction;
}
```
BAM! Done. Now you can `<modifyFunctionality>` wherever you want!

### Inheritance
A traditional inheritance style Transcription Factor interface requires a bit more work to build.
Consider:
```
Animal<>(legs int = 0, makeNoise ()[]{print('NOT IMPLEMENTED';})[]{} //pretend print()[]{} was defined beforehand  
Cat<>(legs int = 4, makeNoise ()[]{print('Meow';})[]{}
```
While you can use `Cat` anywhere you can use `Animal` (and vice versa, in this case), making `Cat` effectively an `Animal`, we shouldn't be duplicating code.
Let's simplify this:
```
AnmialTF<>
{
    object.legs int = 0;
    object.noise string = 'NOT IMPLEMENTED';
    object.makeNoise = ()[]{print(noise);};
}
CatTF< AnimalTF >
{
    object.legs = 4;
    object.noise = 'Meow';
}

main
(
    cat < CatTF > ()[]{}
)
{
    cat.makeNoise();
}
```
Now, we can define any number of Animals through Transcription Factor dependencies and any change in the `AnimalTF` 'base class' will be applied to all Animals.

### Meta Meta
Let's talk a little bit about how the above inheritance system actually works. When a Transcription Factor has a dependency, that dependency is loaded before the execution Block. Thus, the above example of:
```
CatTF< AnimalTF >
{
    object.legs = 4;
    object.noise = 'Meow';
}
```
expands to:
```
CatTF<>
{
    //From AnimalTF
    object.legs int = 0;
    object.noise string = 'NOT IMPLEMENTED';
    object.makeNoise = ()[]{print(noise);};
    
    //From CatTF
    object.legs = 4;
    object.noise = 'Meow';
}
```

We could further expand on this with:
```
KittenTF<CatTF>{object.noise = 'mew';}
```
which would expand to:
```
KittenTF<>
{
    //From AnimalTF
    object.legs int = 0;
    object.noise string = 'NOT IMPLEMENTED';
    object.makeNoise = ()[]{print(noise);};
    
    //From CatTF
    object.legs = 4;
    object.noise = 'Meow';
    
    //From KittenTF
    object.noise = 'mew';
}
```

This code is executed in order, as expected. No tricks.
If we redefine `AnimalTF` to end with the following line: `object.makeNoise()` and write:
```
kitten <KittenTF>()[]{}
kitten.makeNoise();
```
We would get:
```
print('NOT IMPLEMENTED);
print('mew);
```
Since the expanded code would be:
```
KittenTF<>
{
    //From AnimalTF
    object.legs int = 0;
    object.noise string = 'NOT IMPLEMENTED';
    object.makeNoise = ()[]{print(noise);};
    object.makeNoise(); // <--- THE LINE WE ADDED
    
    //From CatTF
    object.legs = 4;
    object.noise = 'Meow';
    
    //From KittenTF
    object.noise = 'mew';
}

main
(
    kitten <KittenTF>()[]{}
)
{
    kitten.makeNoise();
}
```

## Initialization
There are several means by which you might create a constructor. Destructors do not exist in Eons Language of Development but can likewise be accomplished by having a caller call some destructor method.

The easiest way to create a constructor is simply define a TF for your class.
For example, we can break the above example of `AnimalTF`'s call to `makeNoise()` into 2 TFs: a static initialization and functional initialization:
```
Anmial<>
{
    object.legs int = 0;
    object.noise string = 'NOT IMPLEMENTED';
    object.makeNoise = ()[]{print(noise);};
}
AnmialConstructor<>
{
    object.makeNoise();
}

Cat< Animal >
{ 
    object.legs = 4;
    object.noise = 'Meow';
}
CatConstructor< AnimalConstructor > {}

Cat< Animal >
{ 
    object.legs = 4;
    object.noise = 'Meow';
}
CatConstructor< AnimalConstructor > {}

Kitten< Cat >
{ 
    object.noise = 'mew';
}
KittenConstructor< CatConstructor > {}
```
Now, `kitten < Kitten, KittenConstructor >()[]{}` expands to:
```
kitten
<
    //From Animal
    object.legs int = 0;
    object.noise string = 'NOT IMPLEMENTED';
    object.makeNoise = ()[]{print(noise);};
    
    //From Cat
    object.legs = 4;
    object.noise = 'Meow';
    
    //From Kitten
    object.noise = 'mew';
    
    //From AnimalConstructor
   object.makeNoise();
   
   //From CatConstructor
   
   //From KittenConstructor
>()[]{}
```
Which prints the expected 'mew'.

Another way we can create a constructor or destructor is through a Surface definition.
We can say:
```
main
(
    kitten < Kitten >
    (
        constructor ()[]
        {
            makeNoise()
        },
        destructor ()[]
        {
            explode()
        }
    )
    [
        explode ()[]
        {
            print('BOOM!');
        }
    ]
    {}
)
{
    kitten.consturctor();
    kitten.destructor();
}
```
Now, the caller can construct and destruct our `kitten`.

### Meta Initialization
While all variables must be declared on the Surface or Internally before they are used in an execution Block, you can use execution statements to declare variables.
This is valid:
```
MyCell<>
(
    GetSurfaceFor('MyCell').name GetSurfaceFor('MyCell').type = GetSurfaceFor('MyCell').value  
)
[]
{}
```

Note that we cannot include spaces in expressions used in declaration Blocks, so `GetSurfaceFor 'MyCell' GetSurfaceFor 'MyCell' = GetSurfaceFor 'MyCell'` is invalid and will generate an error.
