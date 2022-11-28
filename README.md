# Eons Language of Development

This repo describes the Eons Language of Development specification and provides interpreters where appropriate.

The goal of this language is to provide a concise but powerful means of describing data and operations at any scale. The syntax for iterating over memory addresses in an embedded system should be the same syntax for iterating over servers in a network. 

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
* `''` - String: used for strings.
* `##` - Comment: used for docs & non-evaluated sections of code.
* `[]` - Container: used to manage repeated elements.
* `{}` - Execution: used to define and evaluate functions.
* `()` - Parameter: used to define and bind Surfaces.
* `<>` - Type: used for inheritance and meta programming.

Each Block is allowed to change how symbols are interpreted within it. For example, the Comment Block does not execute code, and adding "{}" inside a string does not define an Execution Block

String and Comment Blocks (`''`, `##`) are considered "non-coding" while all other Blocks are considered "coding".
Type and Execution Blocks are considered "instantiating" while Parameter and Container Blocks are considered "detailing"

### Variations
For compatibility purposes, we support the following variations on Blocks.

#### Strings
You are allowed to use double quotes for a String Block. Though, we don't recommend doing so, mostly because `shift+'` is more work than just `'`.

#### Comments
We don't support any other comment styles at the moment (`/**/` might be good to add in the future).
However, we do support terminating Comment Blocks with the newline character (`\n`), iff (if and only if) there are words after the comment. This means you don't have to remember to always close your Comment Blocks.

`# this is a line comment`

`# this is also a line comment #`

```
#
this is a block comment
#
```

Just don't mix them up:
```
# This will (newline terminates this Comment Block ->)
DESTROY YOUR CODE! (<- supposed to be comment but is now code)
#
everything past this is now a comment.
```

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

#### Container Expansion
Container expansion is done dynamically, depending on what other symbols are adjacent to the Container.
In general, whatever symbol follows the Container will be expanded as a foreach loop of the given operation.

For example, `[1,2]*[3,4]` should yield `[3,4,6,8]`, while `3 + [first, second].my_object` should be equivalent to `3 + first.my_object; 3 + second.my_object`.

You'll see more of this throughout this spec.

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
* `@` - Exit
* `,`, `;`, `\n` (newline) - End.
* `.` - Access, also referred to as spatial separation.
* `\` - Sequence, also referred to as temporal separation.
* `$` - Sigil
* `?` - Condition
* `&` - And
* `|` - Or

The space is a dynamic Operator that is filled in depending on the context of where it is found. See the [Spacing Autofill rules](#spacing-autofill), below.

Besides those for Blocks, these are the only characters used by the Eons Language of Development. All other symbols (e.g. `+`, `-`, `*`, `/`, `%`, etc.) are all user defined and can be changed as thou wilt.

You may also override `<` and `>` for comparisons (and thus `<=`, `>=`, etc.). See [Declaration and Evaluation](#declaration-and-evaluation), below, for more info.

### Exiting and Returns
The Exit Operator exits the current Execution Block, whatever that may be.

`@` behaves as a function, taking arguments. If arguments are provided, the corresponding member variables of the current Functor will be assigned the values given.

There is a default member variable (aka Surface) present in all Functors: `return`. When calling `@(my_var)`, the `return` Surface Binds the `my_var` variable, making it available to other Functors.
If you call `@(first_return=first, second_return=second)`, the first and second return Surfaces will be Bound, as described, leaving the default `return` object untouched.
`@(standard_return, optional_return=extra_information)` is also valid: `return` will be equal to `standard_return` and the `optional_return` Surface will be equal to `extra_information`.
It is not valid to Exit with multiple, unnamed args; if you wish to return a tuple, wrap it in a Container. Meaning, `@(first, second, third)` is invalid and should be `@([first, second, third])`, so that the `return` Surface will be equal to `[first, second, third]`.

>"The exits are at..."

('@' is usually called 'at').

#### The Double Exit Operator
Where `@` means `return`, `@@` means `break`. The idea is that the more work that has to go into typing a statement, the less powerful the statement becomes. So. `@@`, being more work to type than `@`, will only exit the current Execution Block if that Block is a control flow statement and not the Execution Block belonging to a Functor. See [Control Flow](#control-flow), below, for more info.

### Escaping
Still use `\` to escape other characters.

**You should only ever need to escape characters within a string** (e.g. `my_\n_var` is not a valid variable name). Because String Blocks are non-coding, this is fine. Within a string, `\` will not be interpreted as a Sequence, so we maintain it as the escape character.

### Line Endings and Code Separation
Code may be separated by any End Operator. All are equally valid in all contexts, except the newline End (`\n`), which may be used to terminate Comment Blocks.
End Operators are not necessary where a Block terminator is present. For example, `[my,list]` does not need to be `[my,list,]` because the `]` separates the code from whatever may follow.

### Access and Spatial Separation
The Sigil Operator is used to reference both the current object (`$`) and the calling object (`$$`). However, it can only do this when it's not used as a prefix for another symbol.

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
        '$' comes after name to indicate the greater context to which 'name' belongs
        it is also necessary to specify 'name.$', since the local context overrides the parameter.
        #
        name.$ = name
    }
    
    say_hi()
    {
        #
        here, there is no other context to which 'name' could belong beside '$', so no additional specification is necessary.
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
If you prepend a Sequence with the Exit Operator (e.g. `@(find\my\scarf)`), the Sequence will be evaluated and the last Step will be returned from the current Execution Block.

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

### Sigils and References
Objects are normally copied by reference and any change to the object will be changed in all locations.
These changes are thread-safe by default and may wait on other threads.

However, if you would like to copy an object by value (possibly for non-Blocking or destructive access to the object), prefix the Sigil Operator (`$`) to the variable in the variable declaration or whenever you access the object. Using `$` as a prefix will make a copy of the given object for use within the current Execution Block. Using `$` multiple times in the same Execution Block only creates 1 local copy; however, applying the Sigil Operator in multiple Execution Blocks creates a new copy for each.

For example:
```
add($first <int>, second <int>, result <int>)
{
    result = first + $second
    @ result
}
```
Here, `first` and `second` are copied by value and will remain a part of the `add` object until they are unbound.

#### Garbage Collection
When an object has no references, it is deleted.  

#### Accessing the Current and Calling Objects
Other languages use `this` or `self` to indicate the current object. The Eons Language of Development uses a standalone `$`.

Additionally, 2 Sigil Operators (`$$`) indicates the calling Functor.
When one Functor calls another, the caller is made available to the callee through `$$`. In this way, `$` is very similar to `./` in Unix filesystems while `$$` is similar to `../`; in this same manner, 2 callers up would be `$$.$$`, the same way 2 paths up is `../../`.

To demonstrate the difference between `$` as a copy by value indication and `$` as a reference to the current object, consider the example above rewritten more explicitly:
```
add($first <int>, second <int>, result <int>)
{
    result.$ = first.$ + $second.$
    @ result.$
}
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
    int{@ tracking_id}
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

Use `@@` to break out of a control flow Execution Block without exiting the greater Execution Block which contains the statement.
i.e. `@()` means `return` and `@@()` means `break`. You may still set member variables when breaking, as can be done with the Exit Operator.

The `if` statement is defined as `...?{}` and the `if else` statement is defined as `...?{}{}`, where `...` is the condition to check.
Note that the `?` will always cast the preceding statement to `bool`. It is an error if `bool.my_type` returns an `int`, etc.  
There are no `else if` or `elif` statements at this time.

The `while` loop is defined as `(...){}`, where `...` is the condition to run the loop again. Like `if` statements, `while` loops will cast their condition to `bool`.
To exit a while loop, use the Double Exit Operator (`@@`). You may also return a value from a `while` loop with `@(var_to_return)`. Keep in mind that this does not exit the Execution Block which started the loop. You must still 

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

my_colors_and_dogs = [color(name='red'), color(name='blue'), '#00FF00', dog(name='red')]

my_colors_and_dogs[<color>] # gives [color(name='red'), color(name='blue')] #
my_colors_and_dogs[(name='red')] # gives [color(name='red'), dog(name='red')] #
my_colors_and_dogs[<dog>(name='red')] # gives [dog(name='red')] #
```

## Constructors, Destructors, and Lifecycle
Functors are called with `()`. There is no difference between instantiation and execution. When a Functor is called, if the Functor has not been instantiated previously, it will be created automatically and the variables provided in the Parameter Block will override whatever default variables the Functor defined when it was declared.  
In this way, declaring symbols in the Parameter Block of your Functor is as close to a native constructor as we can get.

Likewise, there are no native destructors, and all closing logic should be handled by whatever greater context exists in your program.

However, by convention, `constructor()` is called at the top of a Functor's Execution Block and `destructor()` is called at the bottom. These are not required and you can name them whatever you'd like. In general, we recommend defining `constructor(){}` and `destructor(){}` methods only where appropriate.

Think of the lifecycle of your Functor as existing entirely within it's Execution Block. Every time the Functor is called, it is as if its instantiated anew. You are allowed to cache things between these instantiations but doing so prevents you from destroying them. If you have hardware or even a whole cloud compute cluster that needs to be initialized before your logic, it is highly recommended that you do so in the calling scope and pass the necessary resources to your Functor. Doing this allows the calling scope to tear down those resources when all is done.

## Public, Protected, and Private
By default all members are `public`. However, you can mark members as `protected` or `private` by simply calling the appropriate Functor.
For example,
```
my_class<>
(
    public_member <>

    protected(
        protected_member <>
    )

    private(
        private_member <>
    )
)
```

These Functors are not built in and can be overridden. Likewise, they can be extended; you are welcome to create your own access control statements.
This pattern operates by executing Functors within the Parameter Block. As a result, we can add members to the caller after some modification. In this case, the `protected` and `private` modifications make it such that any access to members provided becomes restricted to either the `my_class` object and its children or to only the `my_class` object, respectively.

## Some Examples

### Calling Add
```
add(first <int>, second <int>, return <int>)
{
    @(first + second)
}

main(three <int>)
{
    # All of these are valid ways to use the `add` Functor.
    three = return.add(1, 2);
    three = add(1, second = 2);
    add(1, 2, three);
    $add(1, 2, return = three);
    #
    Note the lack of a Sigil when using 'three'.
    This will cause add's 'return' to become a reference to 'three' whereby changes to return also change three.
    To prevent this from lingering on subsequent calls to add, we prefix add with the Sigil.
    This makes a copy of the Functor, which is destroyed when the Execution Block terminates.
    #
}
```

### Sorting a Container
```
sort
(
    array <> # Note that we copy by reference, not value.

    private(
        index int,
        buffer <> # we want buffer to be any type, so we mark it as '<>'
    )

{
    array size <= 1 ? {@}
    
    #
    Dhe above statement is dense.
    'array size <= 1' expands to <=.size.array(1),
    Presumably, 'size.array' is an int which gives the number of members in the array Functor (i.e. the number of Surfaces on the Protein).
    The <= Functor would then be defined in the 'int' object.
    The if statement then reads bool.<=.int(int), which should provide the value of return.<=.int(int) as a bool (which it likely already is).
    The Exit Operator (@) is then called if the above bool is true, ending the execution.
    #

    index = 0
    (true) # while loop
    {
        # index + 1 must have spaces and expands to +.index(1)
        # The following becomes: bool.>.array[index](array[+.index(1)]) ? ...
        
        array[index] > array[index + 1] ?
        {
            buffer = array[index]
            array[index] = array[index + 1]
            array[index + 1] = buffer   
        }
        
        index ++ # note the space after 'index', making the expression expand to ++.index().
        index == array size - 1 ? {@@}
    };
}

pair <>
(
    name <string>
    value <int>
    
    int <value> # Type Conversion (for predefined '>' operation)
)

main
(
    heterogeneosu_map <> = [
        var1 <pair>('One', 1)
        var3 <pair>('Three', 3)
        var4 <int>(4)
        var2 <pair>('Two', 2)
    ]
)
{
    sort(heterogeneosu_map);
}
```
This will result in `heterogeneosu_map` being rearranged as:
```
[
    var1 Pair = ('One', 1),
    var2 Pair = ('Two', 2)
    var3 Pair = ('Three', 3),
    var4 int = 4,
]
```
This works on `heterogeneosu_map` with a mixture of Pairs and int(s) just as it would on any data which can be represented as an array of ints. Note that the int requirement only exists because of the `>.int(int)` call, which only takes ints. If we had a map consisting of custom types which implemented `> (other <custom_type>){}`, this would work just as well.

