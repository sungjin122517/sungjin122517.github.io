---
title:  "(OOP) Construction and Destruction"
excerpt: "types of constructors, member initialization list (MIL), destructors, order of constructors and destructors"

categories:
  - oop
tags:
  - [constructors, destructors, MIL, C++]

permalink: /oop/construction-and-destruction/

toc: true
toc_sticky: true
 
date: 2022-08-11
last_modified_at: 2022-08-11
---

## Class object initialization
If all data members of a class are `public`, they can be initialized when they are created using `{}`.  
But what if some of the data members are `private`?  
-> use **CONSTRUCTORS** for initialization! This is because `int main()` function does not have access to private data members. 

<br>

---
## Constructors
Constructor is a <mark>special kind of class member function to initialize an object</mark>.
- It must not specify a return type or explicitly return a value.
- It is called whenever an object is created.

There are 4 different kinds of constructors:
1. Default constructor
2. Conversion coustructor
3. Copy constructor
4. Other constructors

<br>

### Default constructor
Default constructor can be called with `no arguments`.  
It is used to create objects with user-defined `default` values.

```cpp
class Word
{
    private: 
        int frequency;
        char* str;
    public:
        Word() { frequency = 0; str = nullptr; }    // Default constructor
};

int main()
{
    Word movie; // No arguments -> expect default constructor
}
```

If there are no user-defined constructors in the definition of `class X`, <mark>the compiler will generate the following default constructor</mark>:  
    `X::X() {}`   -> this creates an object X with enough space for its data members.

```cpp
class Word
{
    // implicitly private members
    int frequency;
    char* str; 

    // Since no default constructors, the compiler will generate:
    Word::Word() {} // creates a Word object with enough space for its int component and char* component.
};

int main() { Word movie; }
```

<br>

### Conversion constructor
Conversion constructor accepts a `single argument`. It specifies a conversion from its argument type to the type of its class.
- A class may have more than one conversion constructor.
- A constructor may have multiple arguments; if all but `one` argument have `default values`, it is still a conversion constructor.

```cpp
#include <cstring>

class Word
{
    int frequency; char* str;
    public:
        Word(const char* s, int k = 1)  // still conversion constructor, since it can be run with single argument.
        {
            frequency = k;
            str = new char [strlen(s)+1]; strcpy(str, s);
        }
};

int main()
{
    Word *p = new Word {"action"};      // Explicit conversion
    Word movie("Titanic");              // Explicit conversion
    Word director = "James Cameron";    // Implicit conversion

    // For implicit conversion, conversion of its argument type to the type of its class
    Word(const char*): const char* -> Word
}
```

- To disallow unexpected implicit conversion, add the keyword `explicit` before a conversion constructor.
```cpp
class Word
{
    public:
        explicit Word(const char* s, int k = 1) { ... }
}
```

<br>

### Copy constructor
Copy constructor has exactly `one argument` of the `same class` passed by its `const reference`.

```cpp
class Word
{
    private:
        int frequency; char* str;
        void set(int f, const char* s)
            { frequency = f; str = new char [strlen(s)+1]; strcpy(str, s); }
    public:
        Word(const Word& w)     // copy constructor
            { set(w.frequency, w.str); }
};

int main()
{
    Word song(movie);   // parameter passed by value to function
    Word ship = movie;  // object returned by value by function
}
```

`Return value optimization` is a compiler optimization technique which applies `copy elision` in a return statement.  
This means that it omits `copy/move` by constructing a local temporary object directly into the function's return value.

#### Default copy constructor
If <mark>no copy constructor</mark>: the compiler will automatically supply it a `default copy constructor`.  
    X(const X&) { /* memberwise copy */ }

`memberwise copy`: calls the copy constructor of each data member.
e.g. for Word song {movie}:
- copy *movie.frequency* to *song.frequency*
- copy *movie.str* to *song.str*


#### Default memberwise assignment
The default assignment operator '=' will perform memberwise assignment to each data member:
- song.frequency = movie.frequency
- song.str = movie.str

<br>

Memberwise copy와 memberwise assignment의 차이:

```cpp
int main()
{
    Word x("rat");      // 1. conversion constructor
    Word y = x;         // 2. copy constructor
    Word z("cat", 2);   // 3. conversion constructor
    z = x;              // 4. default assignment operator
}
```

- 1과 2같은 경우에선 `memberwise copy`가 일어난다. x라는 Word object가 형성이 되었고, y라는 새로운 object를 형성하는 동시에 x의 정보를 `copy`한다.
- 3과 4같은 경우는 `memberwise assignment`가 일어난다. z라는 Word object가 형성이 되었고, 이미 형성되어있는 z에 x의 정보를 `assign`한다.

<br>
  

### Constructors and function overloading
Constructors are often overloaded.

### Functions with default arguments
Parameters without default values must be declared to the `left` of those with default arguments.

<br>

---
## Member Initializer List (MIL)
Member initializer list (MIL) enables data members of a class to be initialized <mark>before the constructor's function body</mark>, by calling their own constructors.  
The order of the members in the list doesn't matter; the `actual execution order` is their <mark>order in the class declaration</mark>.

```cpp
class Word
{
    private:
        char lang;
        int freq;
        char* str;
    public:
        Word() : lang('E'), freq(0), str(nullptr) { };  // used MIL
        Word(const char* s, int f = 1, char g = 'E') : lang(g), freq(f)  // used MIL
            { str = new char [strlen(s)+1]; strcpy(str, s); }
}
```

<mark>It is better to perform initialization by MIL than by assignments inside constructors</mark>.  
Why? MIL calls the constructors of the data member. Howevever, assignment inside constructors is error-prone.  
The code below is the example.

```cpp
class Word_Pair
{
    private:
        Word w1; Word w2;
    public:
        // 1. MIL: w1 and w2 are initialized using conversion constructor of class Word (check the code above)
        Word_Pair(const char* s1, const char* s2) : w1(s1, 5), w2(s2) { }

        // 2. assignment: error prone because w1 and w2 are initialized using default constructor of class Word, then assignment.
        // assignment operator function may not be properly defined (in case of pointer variables with dynamically allocated memory).
        Word_Pair(const char* x, const char* y) { w1 = x; w2 = y; }   
}
```

- `const` or `reference` members MUST be initialized using MIL if they don't have default initializers.
- MIL always has priority over `default initialization`. This means that if a class has a const data member with default initializers, the const data can be modified using MIL.
- Initialization of const/reference members cannot be done using `default arguments`.

### Delegating constructor
The copy constructor can `delegate` the conversion constructor using `MIL` to create an object.  
The copy constructor is now a delegating constructor.  
**Restriction**: the delegated constructor must be the only item in the MIL.

```cpp
class Word
{
    private:
        int frequency; char* str;
    public:
        Word(const char* s, int f = 1)  // conversion constructor
            { frequency = f; str = new char [strlen(s)+1]; strcpy(str, s); }    // this is same as the function set()
        Word(const Word& w) : Word(w.str, w.frequency)  // copy
}
```

<br>

---
## Garbage Collection & Destructor

### Memory usage on the runtime stack and heap
**Local variables**
- They are constructed when they are defined in a function/block on the `runtime stack`.
- When the function/block terminates, the local variables inside and the call-by-value arguments will be `destructed` and removed on the `runtime stack`.
- Both construction and destruction of variables are done `automatically` by the compiler by calling the appropriate constructors and destructors.

**Dynamically allocated memory**
- It `remains` after function/block terminates, and it is the user's reponsibilty to return it back to the heap for recycling using `delete`; otherwise, it will stay until the program finishes.
- `Garbage`: a piece of storage that is part of a running program but there are no more references to it. Memory leak occurs when there is garbage.

<br>


### Destructor
The destructor of a class is invoked `automatically` <mark>whenever its object goes out of scope</mark>.
- It takes `no arguments`, and has `no return type`.
- There can only be one destructor for a class. This means no overloading is allowed.
- If no destructor is defined, the compiler will automatically generate a `default destructor` which does nothing.
- The destructor itself <mark>does not actually release the object's memory</mark>. It does any assigned things before an object is ready to be destroyed.

### User-defined destructor
User-defined destructors are usually needed when there are pointer members pointing to memory dynamically allocated by constructor of the class.

```cpp
class Word
{
    private:
        int frequency; char* str;
    public:
        Word(const char* s, int k = 0) : frequency(k)
            { str = new char [strlen(s)+1]; strcpy(str, s); }
        ~Word() { delete [] str; }  // destructor member function to deallocate dyn. allocated char array.

}
```

Member functions that are `implicitly generated by the compiler`:
1. default constructor
2. default copy constructor
3. default (copy) assignment operator function
4. default move constructor
5. default move assignment operator function
6. default destructor

If you want to explicitly:
- generate the member functions above: use `= default;`
- not generate the member functions above: use `= delete;` (useful when you don't want any copy constructor)

```cpp
class Word
{
    private: ...
    public:
        Word() = default;
        Word(const Word& w) = delete;   // Words can't be copied. Error will occur if copy constructor is called.
}
```

<br>

---
## Order of Construction and Destruction
**"has" relationship**:
- If an object A has an object B as a data member -> `A has a B`.

**"owns" relationship**:
- If an object A only has a `pointer` pointing to B -> `A owns a B`.
- If B has a memory on the heap, A is responsible for B's destruction.

When an object is constructed, all its `data members` are constructed first.  
The order of destruction is the exact opposite of the order of construction.  

```cpp
class Clock
{
    public: 
        Clock();
        ~Clock();
};

class Postoffice
{
    Clock* clock;
    public:
        Postoffice() { clock = new Clock;}
        ~Postoffice(){ delete clock; }
}

int main()
{
    cout << "Beginning of main\n";
    Postoffice x;
    cout << "End of main\n";
}
```

Order of construction and destruction:
1. Beginning of main
2. Clock constructor
3. Postoffice constructor
4. End of main
5. Postoffice destructor
6. Clock destructor




