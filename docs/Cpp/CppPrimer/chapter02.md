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

```cpp
'a' // character literal
"Hello World!" // string literal
```