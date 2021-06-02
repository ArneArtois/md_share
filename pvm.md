# TYPES

```
T* a ; auto x = *a ; T
T  a ; auto x = &a ; T*
T* a ; auto x = &a ; T**
```



# BITWISE

```
0x12345678 & 0x00000070 == 0x00000070
0x12345678 >> 0x00000004 == 0x01234567 (geen idee)
0x12345678 | 0x123456F8 == 0x123456F8 (fout)
0x12345678 & 0x00005000 == 0x00005000
```



# SYNTAX

```
void foo(T& x);
T* x;

foo(*x);
```

```
void foo(T* x);
const T x;

None of the above works, or it's impossible
```

```
void foo(T& x);
const T x;

None of the above works, or it's impossible
```

```
You are writing a templated function called contains that checks if some value x is an element of some vector<T>
How should x best be passed to this function

const T&
```

```
You need to pass a std::vector<int> to a function. The function does not need to store it somewhere, nor does it want to modify it.

How should you best pass the parameter?
const T&
```

```
You are keeping a central Log object, which is used all over your codebase to write diagnostic messages to.
How you should best pass this log around?

Shared_ptr<T>
```

```
 void foo(char * x);
	char x;
	foo(&x);
```

```
void foo(const char & x);
	std::shared_ptr<char> x;
	foo(*x);
```

```
void foo (const T* x);
const T* x;

foo(x);
```

	void foo(char* x);
	const char& x;
	foo(x*);

```
void foo(char* x);
	const char x;

foo(x*);
```

```
void foo(T& x); 
T& x;

foo(x)
```

```
void foo(const T x);
std::shared_ptr<T> x;

foo(*x)
```

```
E)

You are writing a function with type parameter T. The function expects a value of type T, but only for reading purposes. The function does not store the value for later use.

Antw: const T&
```

```
F)

You are writing a function that takes a std::vector<int> and returns the index of the largest element.

Antw: const T&
```

```
You need to pass a std::vector<double> to a fucntion. The function stores it somewhere for later use and the same vector will also be kept track of in other parts of the code
shared_ptr<T>
```

```
You are creating a templated collection class(such as std::vector<T>), The add method takes an element and copies it ot it's internal data structure
How should this new element best be passed?

const T&
```

```
You are writing a function that takes a std::vector<int> and returns the index of the largest element.

How do you best pass this parameter

const T&
```

```
You are writing a function that takes a std::vector<bool> and negates all bools in the vector. How can you best pass this parameter?

T* 
not : const& / unique ptr / shared_ptr /T
```

```
You need to pass a int to a function. The function does not need to store it somewhere, but it does need to modify its value.

How should you best pass the parameter?

T*
not: shared_ptr / unique ptr
```

You create your own version of std::vector<T>. Internally, you rely on an array in which you store your data. 
whats the best way to store this array inside your custom vector class?

not: T*

```
 You are creating a templated collection class (such as std::vector<T>). The add method takes an element and *copies* it to its internal data structure.How should this new element best be passed?

denk : const T&

not: unique_ptr, T*
```

```
You need to pass a std::vector<double> to a function. The function stores it somewhere for later use and the same vector will still also be kept track of in other parts of the code.

How should you best pass the parameter?

shared_ptr
```

```
You need to pass a std::vector<double> to a function. The function takes over full ownership.

How should you best pass the parameter?

unique_ptr
```

```
You need to pass a bool to a function. The function does not need to store it somewhere, nor does it require write access.How should you best pass the parameter?

T

not const T&
```



```
You need to pass a std::vector<double> to a function. The function stores it somewhere for later use and the same vector will still also be kept track of in other parts of the code.

How should you best pass the parameter?
shared_ptr
```



```
You are dealing with a class hierarchy of shapes, with abstract supertype Shape. A function needs to receive a shape but will not modify it in any way. The function does also not need to store the shape for layer.

How should you best pass the parameter?

const T&
```

```
You are creating a chess application. Pieces are represented by a Piece class, and each Piece object keeps track of an Image object that represents the piece visually. The same Image object is reused for pieces of the same type, e.g., all pawns use the same Image.

How should a Piece object keep track of its corresponding Image?
Shared_ptr
```

```
You need to pass a std::vector<double> to a function. The function takes over full ownership.

unique_ptr<T>
```

```
You are storing a family tree. Each child needs to keep track of both of its parents. We do not want to deal manually with memory management.
How should a child best keep track of its parent?
shared_ptr<T>
```

```
void foo (const T x);
T x;
foo(x);
```

```
void foo (const T& x);
std::unique_ptr<T> x;

foo(*x);
```

```
You are keeping a central Log object, which is used all over your codebase to write diagnostic messages to.

How you should you best pass this log around?
shared_ptr<T>
```

You are writing a function selectYoungerThan that takes a std::vector<Person*> and an age.

How should the age parameter best be passed?



# PRINT

```
#include <iostream>
#define P(x) std::cout << x;


struct Foo{};

struct Bar

{
  void baz(Foo&){P('a');}
  void baz(Foo&) const {P('b');}
  void baz(const Foo&) {P('c');}
  void baz(const Foo&) const {P('d');}
  void baz(Foo*) {P('e');}
  void baz(Foo*) const {P('f');}
  void baz(const Foo*) {P('g');}
  void baz(const Foo*) const {P('h');}
};

int main()
{
  Foo foo;
  const Bar bar;
  bar.baz(foo);
}//b
```

```
#include <iostream>
#define P(x) std::cout << x;


struct Foo

{
  Foo() { P('a'); }
  Foo(const Foo&){ P('b'); }
  ~Foo(){ P('c'); }
};

int main()
{
  P('[');
  Foo foo;
  P(']');
}//[a]c
```

```
#include <iostream>
#define P(x) std::cout << x;


struct Foo

{
  Foo() { P('a'); }
  Foo(const Foo&){ P('b'); }
  ~Foo(){ P('c'); }
};

int main()
{
  P('[');
  Foo x;
  Foo* y = &x;
  P(']');
}//[a]c
```

```
#include <iostream>
#define P(x) std::cout << x;


struct Foo
{
  Foo() { P('a'); }
  Foo(const Foo&){ P('b'); }
  ~Foo(){ P('c'); }
};
void bar(Foo* foo){}

int main()
{
  P('[');
  Foo* p = new Foo;
  bar(p);
   P(']');
}//[a]
```

```
#include <iostream>
#define P(x) std::cout << x;

struct Foo
{
  Foo() { P('a'); }
  Foo(const Foo&){ P('b'); }
  ~Foo(){ P('c'); }
};
void bar(){
    Foo foo;
    }

int main()
{
  P('[');
  Foo foo;
  bar();
   P(']');
}//[aac]c 
```

```
#include <iostream>
#define P(x) std::cout << x;


struct Foo

{
  Foo() { P('a'); }
  Foo(const Foo&){ P('b'); }
  ~Foo(){ P('c'); }
};
void bar(Foo* foo)
{
}

int main()
{
  P('[');
  Foo* p = new Foo;
  bar(p);
  delete p;
  P(']');
}//[ac] 
```

```
#include <iostream>
#define P(x) std::cout << x;


struct Foo

{
  Foo() { P('a'); }
  Foo(const Foo&){ P('b'); }
  ~Foo(){ P('c'); }
};
Foo* bar(Foo* foo)
{
    return foo;
}

int main()
{
  P('[');
  Foo* p = bar(new Foo);
  delete p;
  P(']');
}//[ac]
```

```
#include <iostream>
#define P(x) std::cout << x;


struct Foo{};

struct Bar

{
  void baz(Foo&){P('a');}
  void baz(Foo&) const {P('b');}
  void baz(const Foo&) {P('c');}
  void baz(const Foo&) const {P('d');}
  void baz(Foo*) {P('e');}
  void baz(Foo*) const {P('f');}
  void baz(const Foo*) {P('g');}
  void baz(const Foo*) const {P('h');}
};

int main()
{
  Foo foo;
  Bar bar;
  bar.baz(foo);
}//a
```

```
#include <iostream>
#define P(x) std::cout << x;


struct Foo{};

struct Bar

{
  void baz(Foo&){P('a');}
  void baz(Foo&) const {P('b');}
  void baz(const Foo&) {P('c');}
  void baz(const Foo&) const {P('d');}
  void baz(Foo*) {P('e');}
  void baz(Foo*) const {P('f');}
  void baz(const Foo*) {P('g');}
  void baz(const Foo*) const {P('h');}
};

int main()
{
  const Foo foo;
  Bar bar;
  bar.baz(&foo);
}//g
```

```
#include <iostream>
#define P(x) std::cout << x;


struct Foo{};

struct Bar

{
  void baz(Foo){P('a');}
  void baz(Foo) const {P('b');}
  void baz(Foo*) {P('c');}
  void baz(Foo*) const {P('d');}
  void baz(const Foo*) {P('e');}
  void baz(const Foo*) const {P('f');}
};

int main()
{
  const Foo foo;
  const Bar bar;
  bar.baz(&foo);
}//f
```

```
#include <iostream>
#define P(x) std::cout << x;


struct Foo

{
  Foo() { P('a'); }
  Foo(const Foo&){ P('b'); }
  ~Foo(){ P('c'); }
};

int main()
{
  P('[');
  Foo x;
  Foo y;
  P(']');
}//[aa]cc
```

```
#include <iostream>
#define P(x) std::cout << x;


struct Foo

{
  Foo() { P('a'); }
  Foo(const Foo&){ P('b'); }
  ~Foo(){ P('c'); }
};

int main()
{
  P('[');
  Foo x;
  Foo* y = &x;
  P(']');
}//[a]c
```

```
#include <iostream>
#define P(x) std::cout << x;


struct Foo

{
  Foo() { P('a'); }
  Foo(const Foo&){ P('b'); }
  ~Foo(){ P('c'); }
};
void bar(Foo foo)
{
}

int main()
{
  P('[');
  Foo foo;
  bar(foo);
  P(']');
}//[abc]c
```

```
#include <iostream>
#define P(x) std::cout << x;


struct Foo

{
  Foo() { P('a'); }
  Foo(const Foo&){ P('b'); }
  ~Foo(){ P('c'); }
};
void bar(&Foo foo)
{
}

int main()
{
  P('[');
  Foo foo;
  bar(foo);
  P(']');
}//[a]c
```

```
#include <iostream>
#define P(x) std::cout << x;


struct Foo

{
  Foo() { P('a'); }
  Foo(const Foo&){ P('b'); }
  ~Foo(){ P('c'); }
};

int main()
{
  P('[');
  Foo x;
  Foo y(x);
  P(']');
}//[ab]cc
```

```
#include <iostream>
#define P(x) std::cout << x;


struct Foo

{
  Foo() { P('a'); }
  Foo(const Foo&){ P('b'); }
  ~Foo(){ P('c'); }
};

int main()
{
  P('[');
  Foo* x = new Foo;
  P(']');
}//[a]
```

```
#include <iostream>
#define P(x) std::cout << x;


struct Foo

{
  Foo() { P('a'); }
  Foo(const Foo&){ P('b'); }
  ~Foo(){ P('c'); }
};
Foo* bar(Foo& foo)
{
    return &foo;
}

int main()
{
  P('[');
  Foo foo;
  Foo* p = bar(foo);
  P(']');
}//[a]c
```

```
#include <iostream>
#define P(x) std::cout << x;


struct Foo

{
  Foo() { P('a'); }
  Foo(const Foo&){ P('b'); }
  ~Foo(){ P('c'); }
};
Foo* bar(Foo* foo)
{
    return foo;
}

int main()
{
  P('[');
  Foo foo;
  Foo* p = bar(&foo);
  P(']');
}//[a]c
```

```
#include <iostream>
#define P(x) std::cout << x;


struct Foo

{
  Foo() { P('a'); }
  Foo(const Foo&){ P('b'); }
  ~Foo(){ P('c'); }
};
void bar(Foo* foo)
{
}

int main()
{
  P('[');
  Foo foo;
  bar(&foo);
  P(']');
}//[a]c
```



What is the minimal amount of storage bits needed to store the grades of 150 students?

Grades range from 0 up to (and including) 20.

log2(52^10) * 450 = ceil(resultaat)
