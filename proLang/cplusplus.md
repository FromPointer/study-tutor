##This file mainly contains studying documents of C and C++!

***
###C Language




***
###C++ Language

####C++ New Features
#####1. Lambda Expression
A __lambda expression__ lets you define functions locally, at the place of the call, thereby eliminating much of the tedium and security risks that function objects incur.     

__A lambda expression__ has the form:
    
    [capture](parameters)->return-type {body}

The `[]` construct inside a __function call’s argument list__ indicates the beginning of a __lambda expression__. 
    
    int main() {
        char s[]="Hello World!";
        int Uppercase = 0; //modified by the lambda
        for_each(s, s+sizeof(s), [&Uppercase] (char c) {
            if (isupper(c))
            Uppercase++;
        });
        cout<< Uppercase<<" uppercase letters in: "<< s<<endl;
    }
    

#####2. Automatic Type Deduction and decltype
In __C++03__, you must specify the type of an object when you declare it. Yet in many cases, an object’s declaration includes an initializer. 
__C++11__ takes advantage of this.
letting you declare objects without specifying their types:
    
    auto x=0; //x has type int because 0 is int
    auto c='a'; //char
    auto d=0.5; //double
    auto national_debt=14400000000000LL;//long long

Consider:

    void func(const vector<int> &vi)
    {
        vector<int>::const_iterator ci=vi.begin();
    }

Instead, you can declare the __iterator__ like this:
    
    auto ci=vi.begin()

#####3. Uniform Initialization Syntax
In __C++03__ you can’t initialize __POD__ array members and POD arrays allocated using `new[]`. __C++11__ cleans up this mess with a uniform brace notation:
    
    class C{
        int a;
        int b;
    public:
         C(int i, int j);
     };

    C c {0,0}; //C++11 only. Equivalent to: C c(0,0);
    int* a = new int[3] { 1, 2, 0 }; /C++11 only

    class X {
        int a[4];
    public:
        X() : a{1,2,3,4} {} //C++11, member array initializer
    };



#####4. Deleted and Defaulted Functions
__Function__ in the form:
    
    struct A {
        A()=default; //C++11
        virtual ~A()=default; //C++11
    };
    
is called a defaulted function. The `=default`; part instructs the compiler to generate the default implementation for the function. Defaulted functions have two advantages: They are more efficient than manual implementations, and they rid the programmer from the chore of defining those functions manually.     

The opposite of a defaulted function is a deleted function:
    
    int func()=delete;

__Deleted functions__ are useful for preventing `object copying`, among the rest. Recall that __C++__ automatically declares a copy constructor and an assignment operator for classes. To disable copying, declare these two special member functions `=delete`:

    struct NoCopy {
        NoCopy & operator =( const NoCopy & ) = delete;
        NoCopy ( const NoCopy & ) = delete;
    };
    NoCopy a;
    NoCopy b(a); //compilation error, copy ctor is deleted




#####5. nullptr
At last, __C++__ has a keyword that designates a __null pointer constant__. `nullptr` replaces the bug-prone `NULL` macro and the literal `0` that have been used as __null pointer__ substitutes for many years. `nullptr` is strongly-typed:
   
    void f(int); //#1
    void f(char *);//#2
    
    //C++03
    f(0); //which f is called?
    
    //C++11
    f(nullptr) //unambiguous, calls #2

`nullptr` is applicable to all pointer categories, including `function pointers` and `pointers to members`:
    
    const char *pc=str.c_str(); //data pointers
    if (pc!=nullptr) {
        cout<<pc<<endl;
    }
    int (A::*pmf)()=nullptr; //pointer to member function
    void ( *pmf )()=nullptr; //pointer to function



#####6. Delegating Constructors
In __C++11__ a `constructor` may call `another constructor` of the same class:

    class M {//C++11 delegating constructors
        int x, y;
        char *p;
    public:
        M(int v) : x(v), y(0), p(new char [MAX]) {} //#1 target
        M(): M(0) {cout<<"delegating ctor"<<endl;} //#2 delegating
    };

`Constructor #2`, the __delegating constructor__, invokes the `target constructor #1`.


#####7. Rvalue References
__Reference types__ in __C++03__ can only bind to `lvalues`. __C++11__ introduces a new category of reference types called `rvalue` references. `Rvalue` references can bind to `rvalues`, 

    Eg. __temporary objects__ and __literals__.  

The primary reason for adding `rvalue references` is `move` semantics.    

Unlike traditional `copying`, __moving__ means that a __target object__ pilfers the __resources of the source object__, leaving the __source__ in an __“empty”__ state.

In certain cases where making a copy of an object is both expensive and unnecessary, a `move` operation can be used instead. To appreciate the performance gains of `move` semantics, consider string swapping. A naive implementation would look like this:
    
    void naiveswap(string &a, string & b) {
        string temp = a;
        a=b;
        b=temp;
    }

This is expensive. __Copying a string__ entails the allocation of raw memory and copying the characters from the source to the target. In contrast, __moving strings__ merely swaps two data members, without allocating memory, copying char arrays and deleting memory:

    void moveswapstr(string& empty, string & filled) {
        //pseudo code, but you get the idea
        size_t sz=empty.size();
        const char *p= empty.data();

        //move filled's resources to empty
        empty.setsize(filled.size());
        empty.setdata(filled.data());

        //filled becomes empty
        filled.setsize(sz);
        filled.setdata(p);
    }

If you’re implementing a class that supports moving, you can declare a move constructor and a move assignment operator like this:
    
    class Movable {
        Movable (Movable&&); //move constructor
        Movable&& operator=(Movable&&); //move assignment operator
    };

The C++11 Standard Library uses move semantics extensively. Many algorithms and containers are now move-optimized.


####C++11 Standard Library
__C++__ underwent a major facelift in 2003 in the form of the __Library Technical Report 1 (TR1)__. 
__TR1__ included new container classes (`unordered_set`, `unordered_map`, `unordered_multiset`, and `unordered_multimap`) and several new libraries for `regular expressions`, `tuples`, 
`function object wrapper` and more. With the approval of __C++11__, TR1 is officially incorporated into __C++ standard__, along with new libraries that have been added since __TR1__. 
Here are some of the __C++11__ Standard Library features:

#####1. Threading Library
Unquestionably, the most important addition to __C++11__ from a programmer’s perspective is __concurrency__. 
__C++11__ has a `thread` class that represents an execution `thread`, [promises and futures](http://en.wikipedia.org/wiki/Futures_and_promises),
which are objects that are used for synchronization in a concurrent environment, the [async()](http://www.stdthread.co.uk/doc/headers/future/async.html) function template for launching concurrent tasks, 
and the `thread_local` storage type for declaring `thread-unique` data. For a quick tour of the __C++11__ threading library, read Anthony Williams’ [Simpler Multithreading in C++0x](http://www.devx.com/SpecialReports/Article/38883).



#####2. New Smart Pointer Classes
__C++98__ defined only one __smart pointer__ class, `auto_ptr`, which is now deprecated. __C++11__ includes __new smart pointer__ classes:  `shared_ptr` and the recently-added `unique_ptr`. 
Both are compatible with other __Standard Library__ components, so you can safely store these __smart pointers__ in __standard containers__ and manipulate them with __standard algorithms__.

#####3. New Algorithms
The __C++11__ Standard Library defines new algorithms that mimic the set theory operations `all_of()`, `any_of()` and `none_of()`. The following listing applies the predicate `ispositive()` to the __range [first, first+n)__ and uses `all_of()`, `any_of()` and `none_of()` to examine the range’s propertie


***
###Reference
[C++ Reference Best](http://en.cppreference.com/w/)            
[C Reference](http://www.cplusplus.com/)      
[C++11 Wiki](http://en.wikipedia.org/wiki/C%2B%2B11)        
[stroustrup-C++11FAQ](http://www.stroustrup.com/C++11FAQ.html)       
