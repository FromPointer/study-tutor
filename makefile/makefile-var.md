##Makefile'a main variable and meaning

###Variable definition
    Variable: Using `=` and `define` definition.

    Variable name is sensitive for Case.

    Automatic variable: include special characters.


###Basic of Variable References
#####Uasge:
    $(variable_name) 
#######`or`
    ${variable_name)

###Tow Substitutions of Variable

#### Recursive Substitution(Recursively Expanded)
The first way to difine variable: using `=` or `define`;
    foo = $(bar)
    bar = $(ugh)
    ugh = Huh?
     
    all:
        echo $(foo)

    $make all

Result:
    Huh?
At first $(foo) is substitued by $(bar), then $(bar) is substitued by $(ugh), at last $(ugh) is substitued by Hug?.

####Disadvantage：
1. 使用此风格的变量定义，可能会由于出现变量的递归定义而导致make陷入到无限的变量展开过程中，最终使make执行失败.
######Eg:
    x = $(y)
    y = $(x) $(z)
这种情况下同样会导致make陷入到无限的变量展开过程中。

2. 这种风格变量的定义中如果使引用了某一个函数，那么函数总会在其被引用的地方被执行     

### Direct Substitution(Simply Expanded)
To avoid `Recursive Substitution`, there is another way to define variable. Using `:=` to define.
#####Eg:
    x := foo
    y := $(x) bar
    x := later
is equal to:
    y := foo bar
    x := later

### Special Variable
####1. ?=
`?=` is conditional assignment, if when the variable is not assigned before, it is defined
#####Eg:
    Foo ?= bar 
    <==>
    ifeq ($(origin Foo), undefined)
        Foo = bar
    endif


### Advanced Features
#### Substitution References

A __substitution reference__ substitutes the value of a variable with alterations that you specify. It has the form `$(var:a=b)` (or `${var:a=b}`) and its meaning is to take the value of the variable var, replace every a at the end of a word with b in that value, and substitute the resulting string.
#####Eg:
    foo := a.o b.o c.o
    bar := $(foo:.o=.c)
#####sets `bar` to `a.c b.c c.c`

######Or

    foo := a.o b.o c.o
    bar := $(foo:%.o=%.c)

#### Computed Variable Names



### Appending More Text to Variable
Often it is useful to add more text to the value of a variable already defined. You do this with a line containing `+=`, like this: 
    objects += another.o

#####Eg:
    objects = main.o foo.o bar.o utils.o
    objects += another.o

sets `objects` to `main.o foo.o bar.o utils.o another.o`

Using `+=` is similar to:

    objects = main.o foo.o bar.o utils.o
    objects := $(objects) another.o

but differs in ways that become important when you use more complex values.

When the variable in question has not been defined before, `+=` acts just like normal `=`: it defines a recursively-expanded variable. However, when there is a previous definition, exactly what `+=` does depends on what flavor of variable you defined originally. See section The Two Flavors of Variables, for an explanation of the two flavors of variables.

When you add to a variable's value with `+=`, make acts essentially as if you had included the extra text in the initial definition of the variable. If you defined it first with `:=`, making it a simply-expanded variable, `+=` adds to that simply-expanded definition, and expands the new text before appending it to the old value just as `:=` does (see section Setting Variables, for a full explanation of `:=`).

########In fact,

    variable := value
    variable += more

########is exactly equivalent to:

    variable := value
    variable := $(variable) more

On the other hand, when you use `+=` with a variable that you defined first to be recursively-expanded using plain `=`, make does something a bit different. Recall that when you define a recursively-expanded variable, 
make does not expand the value you set for variable and function references immediately. Instead it stores the text verbatim, and saves these variable and function references to be expanded later, 
when you refer to the new variable (see section The Two Flavors of Variables). When you use `+=` on a recursively-expanded variable, it is this unexpanded text to which make appends the new text you specify.

########
    variable = value
    variable += more

#######is roughly equivalent to:

    temp = value
    variable = $(temp) more

###The `override` Directive
If a variable has been set with a __command argument__, then __ordinary assignments__ in the makefile are ignored. 
If you want to set the variable in the makefile even though it was set with a __command argument__, 
you can use an `override` directive, which is a line that looks like this:
    override variable = value

    or

    override variable := value


###[Variables From The Enviroment](http://ftp.gnu.org/old-gnu/Manuals/make-3.79.1/html_chapter/make_6.html#SEC68)
Variables in `make` can come from the environment in which `make` is run. 
Every environment variable that make sees when it starts up is transformed into a make variable with the same name and value.
But an `explicit assignment` in the makefile, or with a command argument, `overrides` the environment. 

####Target-specific Variable Values


####Pattern-specific Variable Values




####

###[Automatic Variable](https://www.gnu.org/software/make/manual/html_node/Automatic-Variables.html)

####Here is a table of automatic variables:

######1. $@ 
扩展为当前规则的目的文件名      
The file name of the target of the rule. If the target is an archive member, then `$@` is the name of the archive file. 

######2. $% 
当规则的目标文件是一个静态文件时，`$%`代表静态库的一个成员名。例如，某规则的目标是"foo.a(bar.o)",那么，`$%`的值就为"bar.o"，而`$@`的值为"foo.a". 
如果目标不是静态库文件，$%的值为空。       
The target member name, when the target is an archive member. See Archives. For example, if the target is foo.a(bar.o) then `$%` is bar.o and `$@` is foo.a. 
`$%` is empty when the target is not an archive member.

######3. $< 
当前规则的依赖列表的第一个文件,规则的第一个依赖文件名。如果是一个目标文件使用隐含规则来重建，则它代表由隐含规则加入的第一个依赖文件。    
The name of the first prerequisite. If the target got its recipe from an implicit rule, this will be the first prerequisite added by the implicit rule.

######4. $>
它和`$%`一样只适用于库文件，它的值是库名。如果目标不是静态库文件，`$>`的值为空。

######5. $?
所有比目标文件新的依赖文件，以空格分隔。如果目标是静态库文件，代表的库成员。     
The names of all the prerequisites that are newer than the target, with spaces between them. For prerequisites which are archive members, 
only the named member is used .

######6. $^
扩展为当前规则的整个依赖列表      
The names of all the prerequisites, with spaces between them. For prerequisites which are archive members, only the named member is used. 
A target has only one prerequisite on each other file it depends on, no matter how many times each file is listed as a prerequisite. 
So if you list a prerequisite more than once for a target, the value of `$^` contains just one copy of the name. This list does not contain any of the order-only prerequisites; 
for those see the `$|` variable.

######7. $+
类似`$^`,但它保留了依赖文件中重复出现的文件。主要用在程序链接时的库的交叉引用场合.      
This is like `$^`, but prerequisites listed more than once are duplicated in the order they were listed in the makefile.
This is primarily useful for use in linking commands where it is meaningful to repeat library file names in a particular order.

######8. $|
The names of all the order-only prerequisites, with spaces between them.

#####9. $* 它的值是目标文件去掉后缀后的名称
The stem with which an implicit rule matches. If the target is dir/a.foo.b and the target pattern is a.%.b then the stem is dir/foo.
The stem is useful for constructing names of related files.

#####10. Others

    $(@D) The directory part of the file name of the target, with the trailing slash removed. If the value of `$@` is dir/foo.o 
          then `$(@D)` is dir. This value is . if `$@` does not contain a slash.
    $(@F) The file-within-directory part of the file name of the target. If the value of `$@` is dir/foo.o then `$(@F)` is foo.o. `$(@F)` is equivalent to `$(notdir $@)`.
    
    $(*D) The directory part and the file-within-directory part of the stem; dir and foo in this example.
    $(*F)

    $(%D)
    $(%F) The directory part and the file-within-directory part of the target archive member name.

    $(<D)
    $(<F) The directory part and the file-within-directory part of the first prerequisite.

    $(^D)
    $(^F) Lists of the directory parts and the file-within-directory parts of all prerequisites.

    $(+D)
    $(+F) Lists of the directory parts and the file-within-directory parts of all prerequisites, including multiple instances of duplicated prerequisites.

    $(?D)
    $(?F) Lists of the directory parts and the file-within-directory parts of all prerequisites that are newer than the target.
    

####From: [make-06 variable](http://www.yayu.org/book/gnu_make/make-06.html)
