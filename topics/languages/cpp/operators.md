# Time

## Table of Contents
+ [Overloading](#overloading)


## Overloading

**Overloadable operators**:

- Arithmetic: `+`, `-`, `*`, `/`, `%`
- Bitwise: `&`, `|`, `^`, `~`, `<<`, `>>`
- Relational: `==`, `!=`, `<`, `>`, `<=`, `>=`
- Assignment: `=`, `+=`, `-=`, `*=`, `/=`, `%=`, `&=`, `|=`, `^=`, `<<=`, `>>=`
- Increment/decrement: `++`, `--`
- Logical: `!`, `&&`, `||`
- Memory: `new`, `delete`, `new[]`, `delete[]`
- Access and others: `[]`, `()`, `->`, `->*`, `*`, `&`, `,`
- User-defined literal: `""`

**Non-overloadable operators**: `::`, `.`, `.*`, `?:`, `sizeof`, `typeid`, `alignof`, `const_cast`, `static_cast`, `dynamic_cast`, `reinterpret_cast`

**Static operators** (`new`, `delete`, `new[]`, `delete[]`, `""`): Certain operators are static by design, meaning that they're implicitly static, even if not declared that way. They cannot access non-static members of a class directly.

```
class Number
{
  public:
  Number(int v) : value(v) {}

  int value;

  Number operator+(const Number& other) const { return Number(value + other.value); }

  Number operator&(const Number& other) const { return Number(value & other.value); }

  bool operator==(const Number& other) const { return value == other.value; }

  Number& operator+=(const Number& other) { value += other.value; return *this; }

  Number& operator++() { ++value; return *this; }   // prefix ++
  Number operator++(int) { Number temp = *this; ++value; return temp; }   // postfix ++

  bool operator!() const { return value == 0; }

  void* operator new(size_t size) { return new(size); }
  void operator delete(void* ptr) { delete(ptr); }

  int& operator[](int index) const { return arr[index]; }
  Number operator()() const { return *this; }
  Number* operator->() { return this; }
  Number& operator*() { return *this; }
  Number* operator&() { return this; }
  Number operator,(const Number& other) { return other; }

  constexpr long double operator"" _km(long double val) { return val * 1000; }   // auto dist = 5.0_km;  (== 5000.0)
}
```