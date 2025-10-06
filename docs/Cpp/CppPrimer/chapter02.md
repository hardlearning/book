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