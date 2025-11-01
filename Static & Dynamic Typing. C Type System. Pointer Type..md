---
tags:
  - 1stYear
---
# Material: 
- [Lecture](https://moodle.innopolis.university/pluginfile.php/210565/mod_resource/content/1/2024%20ItP%2002%20Introduction%20Pub.pdf)
# Body:
## Static typing:
- The binding between the variable and its type is **hard**: x can take any value but the type of the value must be always the same.
```C
  int x;
  ...
  x = 7; // OK
  ...
  x = "string"; // error
```
- [-]Requires more efforts while writing a program: need to explicitly specify object types.
- [+]The program is (much) more safe: many bugs are detected before running (in compile time).
- [+]The program is more readable; it's easier to read, understand and maintain it.
## Dynamic typing:
- The binding between the variable and its type is soft: x can hold any value of any type.
```JavaScript
  x = 7;
  ...
  x = "string"; // OK
  ...
  y = x + 7 // OK
```
- [+]It's much easier to write a program: no need to take care about object types.
- [+]The program is more flexible: no need to introduce different objects for different purposes.
- [-]The program often looks cryptic; it's required much more efforts to **understand** and **maintain** them.
- [-]**Programs are unsafe and inefficient.**
## Types and Memory:
- What's the size of memory for various types?
```C
int si = sizeof(int);
int se = sizeof a + b;
```
- **Types:**
	- *Fundamental (atomic)* `enum, int, char`
	- *Structured (compound)* `int[10], struct`
	- *Predefined (language-defined)*
	- *Derived ("User-Defined")*
## Pointer - The main type in C:
- **Pointer** is an object containing an address to some other object
```C
int x;
int* p;
...
p = &x; // & - Unary "address-of" operator
```
- **Pointer type** 
```C
T* p; // Declaration of an object of a Pointer
      // type, where T denotes a type pointed
```

- **Operators on pointers:**
	- *Taking address of object* ``
- **More on operators on pointers: *pointer arithmetic***
  `pointer+i`
  `pointer++`
  `ptr1-ptr2`
- **Dynamic Objects & Pointers**
	- **Dynamic Objects** are the ones that are created at any moment during program execution.
	- The lifetime of dynamic objects *is not under the scoping rules.*
	- We can create they by `malloc()` function:
		- `int* p = (int*)malloc(8);`
- **Pointer to Functions:**
```C
void f(int p) {
	...
}
...
void (*pf)(int) = &f;
...
void main() {
	f(1); // call to f
	pf(1);// call to f!	
}
```