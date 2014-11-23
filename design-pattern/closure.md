# Closure Design Patterns 
## Design Patterns
These days I’m learning design patterns. There are a lots of documentation about **software design patterns**, but I’m interesting in closure design patterns.*

Many patterns imply object-orientation, so may not be as applicable in dynamic languages. Peter Norvig demonstrates that 16 out of 23 patterns in the Design Patterns book are simplified or eliminated, [Design Patterns in Dynamic Languages](http://norvig.com/design-patterns/).

I’ve found an interesting presentation of Venkat Subramaniam about [Design Patterns in Java and Groovy](http://www.agiledeveloper.com/presentations/design_patterns_in_java_and_groovy.pdf) and another presentation of Neal Ford about [Design Patterns in Dynamic Languages](http://assets.en.oreilly.com/1/event/27/_Design%20Patterns_%20in%20Dynamic%20Languages%20Presentation.pdf). Here, I extract some patterns of these presentations that involve closures and add others patterns based on my own experience.

\* Groovy makes no such distinction between closures or anonymous functions. I’m really trying to get at is how we can use tools such as first-class functions, lambdas and closures when implementing design patterns.

##Closure Design Patterns
###Execute Around Method
########A pair of operation that needs to be performed before and after operations.

    def operations(closure) {
        println "Open"
        closure()
        println "Close"
    }

    operations { println "Operation" }

    ===> Open
    ===> Operation
    ===> Close

###Pluggable Behavior
########Specify the behavior of an object at runtime.

    def selectValues(number, closure) {
        def list = []
        1.upto(number) {
            if (closure(it)) list << it
        }
        return list
    }

    assert [2, 4, 6, 8, 10] == selectValues(10) { it % 2 == 0 }  // even
    assert [1, 3, 5, 7, 9]  == selectValues(10) { it % 2 != 0 }  // odd
                                   
                                   
###Iterator Pattern
########Allows sequential access to the elements.

    def listNumbers(closure) {
        (0..3).each { closure it }
    }

    listNumbers {
        if (it < 2) println "$it is a little number"
        else println "$it is a big number"
    }

    ===> 0 is a little number
    ===> 1 is a little number
    ===> 2 is a big number
    ===> 3 is a big number
                                               
                                               
###Dynamical Conditional Execution
########Create and execute a conditional operation.

    def greet(user, successClosure, failClosure) {
        if (isAdmin(user)) successClosure()
        else failClosure()
    }

    greet(user, { println "Hi Admin!" }, { println "Hello User" })

###Template Method Pattern
########Define common algorithm steps (getting a customer) and customizations (passed as a closure).

    def withCustomer (id, closure) {
        def customer = getCustomer(id)
        closure(customer)
    }

    withCustomer(1234) { customer ->
        println "Found customer $customer.name"
    }


###Loan Pattern
########Ensures that a resource is deterministically disposed of once it goes out of scope.

    def withListOfWordsForEachLine(file, closure) {
        def reader = file.newReader()
            try {
                reader.splitEachLine(' ', closure)
            } finally {
                reader?.close()
            }
    }

    withListOfWordsForEachLine(file) { wordList ->
        println wordList
    }

###Command Design Pattern
########Encapsulate all the information needed to call a method at a later time.

    def count = 0
    def commands = []

    1.upto(10) {
        commands.add { count++ }
    }

    println "count is initially ${count}"
        commands.each { cmd ->
        cmd()
    }
    println "did all commands, count is ${count}"

    ===> count is initially 0
    ===> did all commands, count is 10


###Strategy Pattern
########Define a family of interchangeable algorithms.

    calcMult = { n, m -> n * m }
    calcAdds = { n, m ->
        def result = 0
        n.times { result += m }
        return result
    }

    def calcStrategies = [calcMult, calcAdds]
    calcStrategies.each { calc ->
        assert 10 == calc(5, 2)
    }


###Factory Pattern
########Abstract the object creation process (currying as a function factory).

    def adder = { x, y -> x + y }
    def incrementer = adder.curry(1)

    assert 5 == incrementer(4)
    
    
###Method Combination
########Build a method from components.

    def sum = { Collection collection -> collection.sum() }
    def first2 = { Collection collection -> collection.take(2) }
    def take2andAdd = first2 >> sum

    assert 3 == take2andAdd([1, 2, 3, 4, 5])

* From: [Closure design pattern](http://qafoo.com/talks/12_10_ipc_closure_design_patterns.pdf)
* From: [Closure-Design-Pattern In Dynamic Languages](http://arturoherrero.com/2012/04/25/closure-design-patterns/)
* From: [Closure-Design-Pattern In JavaScript](http://qafoo.com/talks/12_10_ipc_closure_design_patterns.pdf)
