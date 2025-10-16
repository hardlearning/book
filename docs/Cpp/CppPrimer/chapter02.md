# Chapter 2. Variables and Basic Types

## 2.1. Primitive Built - in Types

### 2.1.1. Arithmetic Types

|Type|Meaning|Minimum Size|
|--|--|--|
|bool|boolean|NA|
|char|character|8 bits|
|wchar_t|wide character|16 bits|
|wchar16_t|Unicode character|16 bits|
|wchar32_t|Unicode character|32 bits|
|short|short integer|16 bits|
|int|integer|16 bits|
|long|long integer|32 bits|
|long long|long integer|64 bits|
|float|single-precision floating-point|6 significant digits|
|double|double-precision floating-point|10 significant digits|
|long double|extended-precision floating-point|10 significant digits|

A char is guaranteed to be big enough to hold numeric values corresponding to the characters in the machine’s basic character set. That is, a char is the same size as a single machine byte. (一个char的大小等于一个机器字节)

The wchar_t type is guaranteed to be large enough to hold any character in the machine’s largest extended character set.

> Machine-Level Representation of the Built-in Types

Computers store data as a *sequence of bits* (比特序列), each holding a 0 or 1.

The smallest chunk of addressable memory is referred to as a “byte”. The basic unit of storage, usually a small number of bytes, is referred to as a “word.” (最小的可寻址内存块被称为字节，基本的存储单元被称为字)

On most machines a byte contains 8 bits and a word is either 32 or 64 bits, that is, 4 or 8 bytes. (大部分机器上1个字节包含8位，一个字包含4或8个字节)


The standard specifies a minimum number of significant digits (有效位数) for floating-point types.

Typically, floats are represented in one word (32 bits), doubles in two words (64 bits), and long doubles in either three or four words (96 or 128 bits). The float and double types typically yield about 7 and 16 significant digits, respectively.

### 2.1.2. Type Conversions

```cpp
bool b = 42; // b is true
int i = b; // i has value 1
i = 3.14; // i has value 3
double pi = i; // pi has value 3.0
unsigned char c = -1; // assuming 8-bit chars, c has value 255
signed char c2 = 256; // assuming 8-bit chars, the value of c2 is undefined
```

- If we assign an out-of-range value to an object of unsigned type, the result is the remainder of the value modulo the number of values the target type can hold. (结果是初始值对无符号类型能表示值的数量取模后的余数) For example, an 8-bit unsigned char can hold values from 0 through 255, inclusive. If we assign a value outside this range, the compiler assigns the remainder of that value modulo 256.
- If we assign an out-of-range value to an object of signed type, the result is undefined.

#### Expressions Involving Unsigned Types

```cpp
unsigned u = 10;
int i = -42;
std::cout << i + i << std::endl; // prints -84
// the int value is converted to unsigned
std::cout << u + i << std::endl; // if 32-bit ints, prints 4294967264
```

Regardless of whether one or both operands are unsigned, if we subtract a value from an unsigned, we must be sure that the result cannot be negative:

```cpp
unsigned u1 = 42, u2 = 10;
std::cout << u1 - u2 << std::endl; // ok: result is 32
std::cout << u2 - u1 << std::endl; // ok: but the result will wrap around
```

### 2.1.3. Literals

#### Integer and Floating-Point Literals

We can write the value 20 in any of the following three ways:

```cpp
20      /* decimal */
024     /* octal */
0x14    /* hexadecimal */
```

> Character and Character String Literals

|Prefix|Meaning|Type|
|--|--|--|
|u|Unicode 16 character|char16_t|
|U|Unicode 32 character|char32_t|
|L|wide character|wchar_t|
|u8|utf-8(string leterals only)|char|

> Integer Literals

|Suffix|MinimumType|
|--|--|
|u or U|unsigned|
|l or L|long|
|ll or LL|long long|

> Floating-Point Literals

|Suffix|MinimumType|
|--|--|
|f or F|float|
|l or L|long double|

Although integer literals may be stored in signed types, technically speaking, the value of a decimal literal is never a negative number. If we write what appears to be a negative decimal literal, for example, -42, the minus sign is not part of the literal.

By default, floating-point literals have type double.

#### Character and Character String Literals

A character enclosed within single quotes is a literal of type char. Zero or more characters enclosed in double quotation marks is a string literal:

```cpp
'a' // character literal
"Hello World!" // string literal
```

The compiler appends a null character ('\0') to every string literal. Thus, the actual size of a string literal is one more than its apparent size.

Two string literals that appear adjacent to one another and that are separated only by spaces, tabs, or newlines are concatenated into a single literal.

```cpp
// multiline string literal
std::cout << "a really, really long string literal "
             "that spans two lines" << std::endl;
```

#### Escape Sequences

An escape sequence begins with a backslash. The language defines several escape sequences:

|Meaning|Escape Sequence|
|--|--|
|newline|\n|
|horizontal tab|\t|
|alert (bell)|\a|
|vertical tab|\v|
|backspace|\b|
|double quote|\\"|
|backslash|\\\\ |
|question mark|\\?|
|single quote|\\'|
|carriage return|\r|
|formfeed|\f|

#### Specifying the Type of a Literal

```cpp
L'a'     // wide character literal, type is wchar_t
u8"hi!"  // utf-8 string literal (utf-8 encodes a Unicode character in 8 bits)
42ULL    // unsigned integer literal, type is unsigned long long
1E-3F    // single-precision floating-point literal, type is float
3.14159L // extended-precision floating-point literal, type is long double
```

#### Boolean and Pointer Literals

The word nullptr is a pointer literal.

## 2.2. Variables

### 2.2.1. Variable Definitions

A definition may (optionally) provide an initial value for one or more of the names it defines:

```cpp
int sum = 0, value, // sum, value, and units_sold have type int
units_sold = 0;     // sum and units_sold have initial value 0
Sales_item item;    // item has type Sales_item (see § 1.5.1 (p. 20))
// string is a library type, representing a variable-length sequence of characters
std::string book("0-201-78345-X"); // book initialized from string
literal
```

#### Initializers

An object that is initialized gets the specified value at the moment it is created.

```cpp
// ok: price is defined and initialized before it is used to initialize discount
double price = 109.99, discount = price * 0.16;
// ok: call applyDiscount and use the return value to initialize salePrice
double salePrice = applyDiscount(price, discount);
```

Initialization is not assignment. Initialization happens when a variable is given a value when it is created. Assignment obliterates an object’s current value and replaces that value with a new one.

#### List Initialization

```cpp
int units_sold = 0;
int units_sold = {0};
int units_sold{0};
int units_sold(0);
```

The form of initialization that uses curly braces is referred to as list initialization.

The compiler will not let us list initialize variables of built-in type if the initializer might lead to the loss of information:

```cpp
long double ld = 3.1415926536;
int a{ld}, b = {ld}; // error: narrowing conversion required
int c(ld), d = ld; // ok: but value will be truncated
```

#### Default Initialization

The value of an object of built-in type that is not explicitly initialized depends on where it is defined. Variables defined outside any function body are initialized to zero. With one exception, variables of built-in type defined inside a function are uninitialized. The value of an uninitialized variable of built-in type is undefined.

Note: Uninitialized objects of built-in type defined inside a function body have undefined value. Objects of class type that we do not explicitly initialize have a value that is defined by the class.

### 2.2.2. Variable Declarations and Definitions

A variable declaration specifies the type and name of a variable. A variable definition is a declaration. In addition to specifying the name and type, a definition also allocates storage and may provide the variable with an initial value.

To obtain a declaration that is not also a definition, we add the extern keyword and may not provide an explicit initializer:

```cpp
extern int i; // declares but does not define i
int j;        // declares and defines j
```

An extern that has an initializer is a definition:

```cpp
extern double pi = 3.1416; // definition
```

It is an error to provide an initializer on an extern inside a function.

Note: Variables must be defined exactly once but can be declared many times.

### 2.2.3. Identifiers

Identifiers in C+ + can be composed of letters, digits, and the underscore character.

The identifiers we define in our own programs may not contain two consecutive underscores, nor can an identifier begin with an underscore followed immediately by an uppercase letter. In addition, identifiers defined outside a function may not begin with an underscore.

### 2.2.4. Scope of a Name

A scope is a part of the program in which a name has a particular meaning. Most scopes in C+ + are delimited by curly braces.

#### Nested Scopes

Names declared in the outer scope can also be redefined in an inner scope:

```cpp
#include <iostream>
// Program for illustration purposes only: It is bad style for a function
// to use a global variable and also define a local variable with the same name
int reused = 42; // reused has global scope
int main()
{
    int unique = 0; // unique has block scope
    // output #1: uses global reused; prints 42 0
    std::cout << reused << " " << unique << std::endl;
    int reused = 0; // new, local object named reused hides global reused
    // output #2: uses local reused; prints 0 0
    std::cout << reused << " " << unique << std::endl;
    // output #3: explicitly requests the global reused; prints 42 0
    std::cout << ::reused << " " << unique << std::endl;
    return 0;
}
```

## 2.3. Compound Types

### 2.3.1. References

A reference defines an alternative name for an object.

```cpp
int ival = 1024;
int &refVal = ival; // refVal refers to (is another name for) ival
int &refVal2;       // error: a reference must be initialized
```

When we define a reference, instead of copying the initializer's value, we bind the reference to its initializer.

There is no way to rebind a reference to refer to a different object.

#### A Reference Is an Alias

After a reference has been defined, all operations on that reference are actually operations on the object to which the reference is bound:

```cpp
refVal = 2; // assigns 2 to the object to which refVal refers, i.e., to ival
int ii = refVal; // same as ii = ival

// ok: refVal3 is bound to the object to which refVal is bound, i.e., to ival
int &refVal3 = refVal;
// initializes i from the value in the object to which refVal is bound
int i = refVal; // ok: initializes i to the same value as ival
```

#### Reference Definitions

We can define multiple references in a single definition. Each identifier that is a reference must be preceded by the & symbol:

```cpp
int i = 1024, i2 = 2048; // i and i2 are both ints
int &r = i, r2 = i2;     // r is a reference bound to i; r2 is an int
int i3 = 1024, &ri = i3; // i3 is an int; ri is a reference bound to i3
int &r3 = i3, &r4 = i2;  // both r3 and r4 are references
```

The type of a reference and the object to which the reference refers must match exactly.

A reference may be bound only to an object, not to a literal or to the result of a more general expression:

```cpp
int &refVal4 = 10; // error: initializer must be an object
double dval = 3.14;
int &refVal5 = dval; // error: initializer must be an int object
```

### 2.3.2. Pointers

Like references, pointers are used for indirect access to other objects. Unlike a reference, a pointer is an object in its own right.

```cpp
int *ip1, *ip2;  // both ip1 and ip2 are pointers to int
double dp, *dp2; // dp2 is a pointer to double; dp is a double
```

#### Taking the Address of an Object

We get the address of an object by usin the address-of operator (the & operator):

```cpp
int ival = 42;
int *p = &ival; // p holds the address of ival; p is a pointer to ival
```

Because references are not objects, they don’t have addresses. Hence, we may not define a pointer to a reference.

The types of the pointer and the object to which it points must match:

```cpp
double dval;
double *pd = &dval; // ok: initializer is the address of a double
double *pd2 = pd;   // ok: initializer is a pointer to double
int *pi = pd; // error: types of pi and pd differ
pi = &dval;   // error: assigning the address of a double to a pointer to int
```

#### Pointer Value

The value stored in a pointer can be in one of four states:

1. It can point to an object.
2. It can point to the location just immediately past the end of an object.
3. It can be a null pointer, indicating that it is not bound to any object.
4. It can be invalid; values other than the preceding three are invalid.

It is an error to copy or otherwise try to access the value of an invalid pointer. The result of accessing an invalid pointer is undefined.

Because pointers in cases 2 and 3 do not point to any object, we may not use them to access the (supposed) object to which the pointer points. If we do attempt to access an object through such pointers, the behavior is undefined.

#### Using a Pointer to Access an Object

When a pointer points to an object, we can use the dereference operator (the * operator) to access that object:

```cpp
int ival = 42;
int *p = &ival; // p holds the address of ival; p is a pointer to ival
cout << *p;     // * yields the object to which p points; prints 42

*p = 0; // * yields the object; we assign a new value to ival through p
cout << *p; // prints 0
```

> Key Concept: Some Symbols Have Multiple Meanings

```cpp
int i = 42;
int &r = i;   // & follows a type and is part of a declaration; r is a reference
int *p;       // * follows a type and is part of a declaration; p is a pointer
p = &i;       // & is used in an expression as the address-of operator
*p = i;       // * is used in an expression as the dereference operator
int &r2 = *p; // & is part of the declaration; * is the dereference operator
```

#### Null Pointers

```cpp
int *p1 = nullptr; // equivalent to int *p1 = 0;
int *p2 = 0; // directly initializes p2 from the literal constant 0
// must #include cstdlib
int *p3 = NULL; // equivalent to int *p3 = 0;
```

`nullptr` is a literal that has a special type that can be converted to any other pointer type.

Older programs sometimes use a preprocessor variable named `NULL`, which the cstdlib header defines as 0.

When we use a preprocessor variable, the preprocessor automatically replaces the variable by its value. Hence, initializing a pointer to NULL is equivalent to initializing it to 0.

It is illegal to assign an int variable to a pointer, even if the variable’s value happens to be 0.

```cpp
int zero = 0;
pi = zero; // error: cannot assign an int to a pointer
```

> Advice: Initialize all Pointers

Uninitialized pointers are a common source of run-time errors.

If there is no object to bind to a pointer, then initialize the pointer to nullptr or zero. That way, the program can detect that the pointer does not point to an object.

#### Assignment and Pointers

Assignment makes the pointer point to a different object:

```cpp
int i = 42;
int *pi = 0; // pi is initialized but addresses no object
int *pi2 = &i; // pi2 initialized to hold the address of i
int *pi3; // if pi3 is defined inside a block, pi3 is uninitialized
pi3 = pi2; // pi3 and pi2 address the same object, e.g., i
pi2 = 0; // pi2 now addresses no object
```

The important thing to keep in mind is that assignment changes its left -hand operand.

```cpp
pi = &ival; // value in pi is changed; pi now points to ival
*pi = 0;    // value in ival is changed; pi is unchanged
```

#### Other Pointer Operations

If the pointer is 0, then the condition is false:

```cpp
int ival = 1024;
int *pi = 0; // pi is a valid, null pointer
int *pi2 = &ival; // pi2 is a valid pointer that holds the address of ival
if (pi) // pi has value 0, so condition evaluates as false
    // ...
if (pi2) // pi2 points to ival, so it is not 0; the condition evaluates as true
    // ...
```

Two pointers are equal if they hold the same address and unequal otherwise. Two pointers hold the same address if they are both null, if they address the same object, or if they are both pointers one past the same object.

#### void* Pointers

The type void* is a special pointer type that can hold the address of any object.

```cpp
double obj = 3.14, *pd = &obj;
// ok: void* can hold the address value of any data pointer type
void *pv = &obj; // obj can be an object of any type
pv = pd; // pv can hold a pointer to any type
```

There are only a limited number of things we can do with a void* pointer: We can compare it to another pointer, we can pass it to or return it from a function, and we can assign it to another void* pointer. We cannot use a void* to operate on the object it addresses.

### 2.3.3. Understanding Compound Type Declarations
