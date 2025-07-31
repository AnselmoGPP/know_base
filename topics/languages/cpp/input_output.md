# Input/Output

## Table of Contents
+ [IO classes](#io-classes)
  + [IO types](#io-types)
  + [Condition states](#condition-states)
  + [The output buffer](#the-output-buffer)
  + [Manipulators](#manipulators)
+ [File IO](#file-io)
  +[Classes](#classes)
  +[File modes](#file-modes)
  +[Write (output)](#write-(output))
  +[Read (input)](#read-(input))
  +[Positioning](#positioning)
+ [String streams](#string-streams)


## IO classes


### IO types

**Stream**: Class that represents a sequence of characters (bytes) coming from an input source (file, keyboard, socket...) or going to an output destination (file, screen...). It's an abstraction used for I/O operations, enabling you to read from and write to various data sources in a consistent and flexible way. This abstracts away the specifics of data sources and destinations, letting you interact with them in a similar way regardless of the underlying details. 

IO is handled by a family of stream types defined in the SL. These types support IO to and from devices. It defines operations to read and write values of the built-in types. Classes (such as strings) define similar IO operation to work on objects of their class type. By default, the IO types and objects we have used for manipulating char data are connected to the user’s console window. IO headers and library types:

- `<iostream>`: Defines the basic types (parents classes) used to read from and write to a _stream_.

  - `istream`, `wistream`: Reads from a stream.
  - `ostream`, `wostream`: Writes to a stream.
  - `iostream`, `wiostream`: Reads and writes a stream.

- `<fstream>`: Defines the types used to read and write _named files_.

  - `ifstream`, `wifstream`: Reads from a file.
  - `ofstream`, `wofstream`: Writes to a file.
  - `fstream`, `wfstream`: Reads and writes a file.

- `<sstream>`: Defines the types used to read and write _in-memory strings_.

  - `istringstream`, `wistringstream`: Reads from a string.
  - `ostringstream`, `wostringstream`: Writes to a string.
  - `stringstream`, `wstringstream`: Reads and writes a string.

Standard streams: Preconnected input/output communication channels between our program and other devices (keyboard, screen...).

- `stdin` (`cin`): Standard input. Associated with the standard input devices (usually the keyboard).
- `stdout` (`cout`): Standard output. Associated with the standard output device (usually the display screen).
- `stderr` (`cerr`, `clog`): Standard error. Associated with the standard error stream. Used for error messages and diagnostic output.

`<iostream>` defines some elements:

  - Objects:

    - `cin`: istream object that reads from `stdin`.
    - `cout`: ostream object that writes to `stdout`.
    - `cerr`: ostream object that writes to `stderr`.
    - `clog`: ostream object that writes to a buffer before writing it to `stderr`.

  - Operators:  

    - `>>`: Extraction operator. Used to read input from an istream object. It takes 2 operands: istream object (left) and another object (right). It reads from the istream object, stores data in the other object, and returns the istream object. 
    - `<<`: Insertion operator. Used to write output to an ostream object. It takes 2 operands: ostream object (left) and value to print (right). It writes the value on the ostream object and returns the ostream object.

  - Functions:

    - `cin::ignore(args)`: Discard a specified number of characters from the input buffer. If `args` is empty, it clears `cin`. If `args` == number, it discards that number of characters or until a newline (`\n`). If `args` == number and character (delimiter), it discards that number of characters or until the delimiter is found.

```
double price;
cin  << price;
cout << price << std::endl;
```

`<string>` defines some elements:

- `getline` (`<string>`): Function that reads a line of input from a given istream into a given string.
- `<<` and `>>` operators: They allow to input/output strings to/from a stream.

```
string s;
cin >> s;   // get single word (stops at first whitespace character).
getline(cin, s);   // get entire line
```

```
string word;
cin >> word;   // stores a single word (stops at first whitespace character).

cin.ignore();   // removes \n character
string manyWords;
getline(cin,  manyWords);   // stores many words in a string (doesn't stop at whitespaces)
```

Explanation: `>>` leaves the `\n` in the input stream, while `getline` discards it. So, when `getline` reads, it encounters a `\n` as the first character and stops reading. So, `cin.ignore` is required for discarding the `\n` character

The types and objects that manipulate wchar_t data begin with w (wcin, wcout, wcerr …).

**Inheritance**: Programming feature that lets a type inherit the interface of another type.

Neither the kind of device (console window, disk file, string…) nor the character size (char, wchar_t…) affects the IO operations we can perform. The library let us ignore the differences among these different kinds of streams by using **inheritance**. Example: types ifstream and istringstream inherit from istream, so we can use objects of type ifstream or istringstream as if they were istream objects. We can use these objects in the same way we use cin, >>, getline, etc. Similarly, ofstream and ostringstream inherit from ostream.

`fstream` and `stringstream` classes are related by inheritance to `iostream` classes.

- The **input** classes inherit from `istream` (`ifstream` and `istringstream` inherit from `istream`). Thus, operations that can be performed on an `istream` object can also be performed on either an `ifstream` or an `istringstream`.
- The **output** classes inherit from `ostream` (`ofstream` and `ostringstream` inherit from `ostream`). Thus, operations that can be performed on an `ostream` object can also be performed on either an `ofstream` or an `ostringstream`.

Each IO object maintains a set of condition states that indicate whether IO can be done through this object. If an error is encountered (such as hitting EOF on an input stream), the object’s state will be such that no further input can be done until the error is rectified. The library provides a set of functions to set and test these states.

Everything that follows applies equally to plain streams, file streams, string streams and char or wide-char streams.

We **cannot copy or assign** objects of the IO types; therefore, we cannot have a parameter or return type that is one of the stream types. Functions that do IO typically pass and return the stream through references. Reading or writing an IO object changes its state, so the reference must not be const.


### Condition states

Errors can occur. A stream has a certain condition state that indicate whether a given stream is usable. The IO classes define **functions and flags** that let us access and manipulate the **condition state** of a stream.

If we enter on the standard input a **variable of a type that the input operator doesn’t expect to read**, cin will be put in an error state.

```
int val;
cin >> val;   // If we enter "bool", input operator gets B and cin is put in an error state
```

Once, an error has occurred, subsequent IO operations on that stream will fail. We can read from or write to a stream only when it’s in a non-error state. Your code should **check whether a stream is OK** before attempting to use it. Easiest way: Using a stream as a condition.

```
while(cin >> word)
```

If that input operation succeeds, the state remains valid and the condition succeeds.

**How do we know WHY the stream is invalid?**

The IO library defines a machine-dependent **integral type** named `std::iostate` that conveys information about the state of a stream. It is used as a collection of bits. The IO classes define four `constexpr` values of type iostate that represent particular bit patterns. These values are used to indicate particular kinds of IO conditions. They can be used with the bitwise operators to test or set multiple flags in one operation.

```
// strm represents one of the previous types from iostream, fstream or sstream.
strm::iostate

// strm::iostate values:
strm::badbit
strm::failbit
strm::eofbit
strm::goodbit
```

- `iostate`: Machine-dependent integral type. Represents the condition state of a stream.

  - `badbit`: System-level failure (stream is corrupted), such as an unrecoverable read or write error. It’s usually not possible to use a stream once badbit has been set.
  - `failbit`: Recoverable error (an IO operation failed), such as reading a character when numeric data was expected. It’s often possible to correct it and use the stream again.
  - `eofbit`: Reaching end-of-file sets both eofbit and failbit.
  - `goodbit`: Indicates no failures on the stream. Guaranteed to be 0.

If `badbit`, `failbit` or `eofbit` is set, the condition that evaluates that stream will fail.

The library also defines a set of **functions to interrogate the state** of these flags (s is the stream):

```
s.bad()
s.fail()
s.eof()
s.good()
s.clear()
s.clear(flags)
s.setstate(flags)
s.rdstate()
```

- `bad()`: True if badbit in the stream s is set
- `fail()`: True if failbit or badbit in the stream s is set
- `eof()`: True if eofbit in the stream s is set
- `good()`: True if none of the error bits is set

`good` or `fail` are used to determine the overall state of a stream. To use a stream as a condition is equivalent to `!fail()`. The `eof` and `bad` operations reveal only whether those specific errors have occurred.

- `clear()`: Reset all condition values in the stream s to valid state.
- `clear(flags)`: Reset the condition of s to flags. This is overloaded: one version takes no arguments (turns off all the failure bits), another takes a single argument of type iostate. Returns void.
- `setstate(flags)`: Adds specified condition/s to s (turns on the given condition bit/s to indicate that a problem occurred). Type of flags is iostate. Returns void.
- `rdstate()`: Returns current condition of s as an iostate value.

How to use `s.clear()` (version with no argument):

```
auto old_state = cin.rdstate();  // Save current state of cin
cin.clear();                     // Make cin valid
process_input(cin);              // Use cin
cin.setstate(old_state);         // Reset cin to its old state
```

To turn off a single condition, we use clear() (taking an argument) and the bitwise operators to produce the desire new state:

```
cin.clear(cin.rdstate() & ~cin.failbit & ~cin.badbit);
```


### The output buffer

Each output stream manages a buffer, which it uses to hold the data that the program reads and writes.

```
os << "Hi there";
```

**Flush**

The literal string might be printed immediately or the operating system might store the data in a buffer to be printed later (this allows the operative system to combine several output operations into a single system-level write). There are several conditions that cause the buffer to be **flushed** (i.e. to be written) to the actual output device or file:

- Program completes _normally_. All output buffers are flushed as part of the `return` from `main`.
- The buffer becomes _full_, so it’s flushed before writing the next value.
- We flush the buffer explicitly with `endl` (or _flush_, or _ends_).

```
cout << "hi" << flush; // Flushes the buffer and adds no data
cout << "hi" << endl; // Writes a newline and flushes the buffer
cout << "hi" << ends; // Writes a null and flushes the buffer
```

- We use `unitbuf` manipulator to set the stream’s internal state to empty the buffer after each output operation. By default, unitbuf is set for cerr, so writes to cerr are flushed immediately. Use `nounitbuf` for restoring the stream to use normal, system-managed buffer flushing.

```
cout << unitbuf;
cout << nounitbuf;
```

Output buffers are not flushed if the program terminates abnormally. If it crashes, it’s likely that data the program wrote may be sitting in an output buffer waiting to be printed. When you debug a crashed program, make sure that any output you think should have been written was actually flushed.

**Tie**

Tying Input and Output streams together:

If the input stream is tied to an output stream, any attempt to read the input stream will first flush the buffer associated with the output stream (usual in interactive systems, so the prompts to the user are written before attempting to read the input). By default, cin and cout are tied by the library. Two overloaded versions of **tie**:

- Take _no arguments_: Returns a pointer to the output stream, if any, to which this object is currently tied. Returns a null pointer if the stream is not tied.
- Takes a _pointer to an ostream_: Ties itself to that ostream. If the argument is a `nullptr`, the stream is untied completely.

```
x.tie(&o);       // Ties stream x to the output stream o
```

We can tie either an `istream` or an `ostream` object to another `ostream`. Each stream can be tied to at most one stream at a time. However, multiple streams can tie themselves to the same `ostream`.

```
cin.tie(&cout);                       // Library already ties cin and cout by default
ostream *old_tie = cin.tie(nullptr);  // Untie cin. oldtie points to the stream tied to cin, if any
cin.tie(&cerr);
cin.tie(old_tie);                     // Reestablish normal tie between cin and cout
```


### Manipulators

**Manipulators**: Predefined objects that you pass to the stream to format the way output is displayed on a stream.

**<iostring>**

- `std::flush`: Flush internal buffer to the physical device (console…) immediately. Useful for displaying debugging information.  It ensures all the output generated so far is written to the output stream, rather than sitting in memory waiting to be written. If you don’t flush the stream, if the program crashes, output may be left in the buffer, leading to incorrect inferences about where the program crashed.

```
std::cout << "Debug message. Value of x is " << x << std::flush;
```

- `std::endl`: End-of-line character + flush buffer.

```
std::cout << "Hello world << std::endl;
```

**<iomanip>**

- **Field width**: Set the minimum field width for the next value displayed on the stream (only applies to the next value). Default value is 0. It doesn’t cause truncation.

```
const char * message = "hi you";
std::cout << std::setw(10) << message << std::endl;     // [....hi you]
```

- **Control justification**: Right justified by default. Applies to all subsequent values.

```
std::cout << std::left;
std::cout << std::setw(10) << "hello" ≺≺ std::endl;   // [hello.....]
std::cout << std::right;
std::cout << std::setw(10) << "world" ≺≺ std::endl;   // [.....hello]
```

- **Numeric sign justification**: Justifies numeric values within the field width. The sign (+ or -) is left-justified, the number is right-justified. Applies to all subsequent values.

```
std::cout << std::internal;
std::cout << std::setw(10) << -35 << std::endl;
```

```
-.......35
```

- **Formatting floating-point** values:

  - _Fixed_ format: `23.98970`
  - _Scientific_ format: `1.23e5`
  - _General_ format (default): Varies depending on number size.

```
double pi = 3.14159265358979;
std::cout << std::fixed;
std::cout << pi << std::endl;
std::cout << std::scientific;
std::cout << pi << std::endl;
std::cout.unsetf(std::ios::fixed | std::ios::scientific);   // re-establish general formatting
std::cout << pi << std::endl;
```

```
3.141593
3.141593e+00
3.14159
```

They apply to all subsequent values.

- **Precision**: Determine the precision for all subsequent output values. Varies depending on the format you are using.

  - General: Number of significant digits.
  - Fixed/scientific: Number of digits after decimal point.

```
std::cout << std::setprecision(4);
std::cout << 3.1415926536;
```

```
3.142
```

- **Show positive sign**: Specify whether you want the + sign to be displayed alongside positive numbers (not displayed by default). Applies to all subsequent values.

```
std::cout << std::showpos;
std::cout << 33 << std::endl;
std::cout << std::noshowpos;
std::cout << 33 << std::endl;
```

```
+33
33
```

- **Hexadecimal/Octal numbers**:

- `oct`, `hex`, `dec`: Specify whether numbers are formatted in decimal (default), octal or hexadecimal. 
- `showbase`, `noshowbase`: Specify whether to display or not the number base alongside the numbers (leading **0** for octal, leading **0x** for hexadecimal).
- `uppercase`, `nouppercase`: Format numbers with uppercase letters.
- All this applies to all subsequent values.

```
std::cout << std::showbase;
std::cout << std::uppercase;
std::cout << 64 ≺≺ std::endl;
std::cout << std::oct << 64 << std::endl;
std::cout << std::hex << 64 << std::endl;
std::cout << std::dec << 64 << std::endl;
std::cout << std::noshowbase;
std::cout << std::nouppercase;
```

```
64
0100
0X40
64
```


## File IO

### Classes

`<fstream>` header defines 3 stream-based classes for reading/writing to/from files:

- `ifstream`: Read from a file using `>>`.
- `ofstream`: Write to a file using `<<`.
- `fstream`: Reads and writes from/to a file using `>>` and `<<`.

They inherit from the `iostream` types the same operations as those we used with `cin` and `cout` (`<<`, `>>`, `getline`…). They also add new members:

```
fstream fstrm;              // Creates an unbound file stream
fstream fstrm(s);           // Open a file named s
fstream fstrm(s, mode);

fstrm.open(s);
fstrm.open(s, mode);
fstrm.close();
fstrm.is_open();
```

- `fstream`

  - `fstream fstrm`: Create an unbound file stream.
  - `fstream fstrm(s)`: Create a file stream and open the file named s (s can have type string or be a pointer to a C-style char string). The default file mode depends on the type of `fstream`. These constructors are `explicit`.
  - `fstream fstrm(s, mode)`: The same, but opens s in the given mode.

### Open/Close

  - `.open(s)`: Opens the file named s and binds that file to fstrm (s can have type string or be a pointer to a C-style char string). The default file mode depends on the type of fstream. Returns void.
  - `.open(s, mode)`: The same, but opens s in the given mode.
  - `.close()`: Close the file to which `fstrm` is bound. Returns `void`.
  - `.is_open()`: Returns a `bool` true if the file associated with `fstrm` is open.

For reading/writing a file, we define a file stream object and associate that object with the file. If we supply a file name in the creation of the file stream object, `open()` is called automatically. File names can be either library strings or C-style character arrays.

```
fstream file("file.txt");   // or file.open("file.txt");
if(file.is_open())
{
  // do something
  file.close();
}
```

We can use an object of an inherited type in places where an object of the original type is expected. So, if a function takes a reference (or pointer) to one `iostream` type, this function can be called on behalf of the corresponding `fstream` (or `sstream`) type. That is, if our function takes an `ostream&`, we can call it passing an `ofstream` object; similarly, for `istream&` and `ifstream`.

```
ifstream input(argv[1]);
ofstream output(argv[2]);
Sales_data total;

if(read(input, total)){                         // read first transaction
     Sales_data trans;
     while(read(input, trans)) {                // read remaining transactions
          if(total.isbn() == trans.isbn()) total.combine(trans);
          else {
               print(output, total) << endl;    // Print result
               total = trans;
          }
     }
     print(output, total) << endl;              // Print last transaction
}
else cerr << "No data" << endl;
```

We can pass our fstream objects to `read()` and `print()` even though the parameters to those functions are defined as `istream&` and `ostream&` respectively.

```
ifstream in(ifile);           // Open file
ofstream out;                 // File stream not associated with a file
out.open(ifile + ".copy");    // Open file
```

If a call to `open()` fails, `failbit` is set. If succeeds, `open()` set the stream’s state so that `good()` is true. So, it’s recommended to verify that the `open()` succeded.

```
if(out)    // This condition is true if open() succeeds
```

Calling `open()` on a file stream that is already open will fail and set the `failbit`. Subsequent attempts to use that file stream will fail. To associate a file stream with a different file, we must first close the existing file and then open the new one.

When a `fstream` object is destroyed (goes out of scope), close() is called automatically.

**C-style** way of managing a file:

```
FILE* fptr;
char filename[256];

if(fptr = fopen(filename, "r"))   // r: read, w: write
{
  char line[256];
  while(fgets(line, 256, fptr))
    { /*do something*/ }
  fclose(fptr);
}
```

### File modes

Each stream has a file mode (a `std::ios_base` flag) that represents how the file may be used, and it’s defined by the fstream class when opening a file. We can supply a file mode whenever we open a file (by constructor or by `open()`).

- `in`: Open for input. Only available for ifstream or fstream.
- `out`: Open for output. Only available for ofstream or fstream. Discards the contents of the file, unless we specify app.
- `app`: All output operations will occur at the end of file, so existing content is preserved. Available if trunc is not set. If app is specified, the file is always opened in output mode.
- `ate`: The initial position (position immediately after the open) for read/write set at the end of file (default is the start).
- `trunc`: Truncate the file (if you open file for output, its contents will be deleted and replaced). Only available when out is also specified.
- `binary`: Do IO operations in binary mode (no formatting applied to values when read or written). Binary files are typically smaller than text files and can more efficient to read and write.

Combine modes using **bitwise OR operator |**.

Each file stream type defines a default file mode: `ifstream` (in), `ofstream` (out, trunc), `fstream` (in, out). The only way to preserve the existing data in a file opened by an `ofstream` is to specify `app` or `in` mode explicitly.

```
ofstream out1("file1");                   // out and trunc are implicit
ofstream out2("file1", ofstream::out);    // trunc is implicit
ofstream out3("file1", ofstream::out | ofstream::trunc);
```

```
ofstream app1("file2", ofstream::app);    // out is implicit
ofstream app2("file2", ofstream::out | ofstream::app);
```

Any time `open()` is called, the file mode is set (either explicitly or implicitly). When not specified, the default value is used. The file mode of a given stream may change each time a file is opened (`open()`).

```
ofstream out;               // no file mode set
out.open("file_1");         // mode implicitly out and trunc (out implies trunc)
out.close();
out.open("file_2", ofstream::app);  // mode is out and app
```

### Write (output)

- `<<` operator: Can be used to write strings and **formatted** data. Ensure that values are separated from each other (example: with spaces). We write a **newline** character (`\n`) at the end of each record (indicates end and beginning of a record); except for the final record, which has an **end-of-file** (indicates there's no more data).

```
ofstream ofile("file.txt");
ofile << "Here is line 1" << endl;
ofile << "Here is line 2" << endl;
ofile.close();
```

```
string str{" is "};
ofile << "John" << " " << str << " " << 1.74 << endl;
ofile << "Jane" << " " << str << " " << 1.55;
```

```
int a = 64, b = 128;
string str;

str += to_string((unsigned long long)a);
str += " ";
str += to_string((unsigned long long)b);
str += "\n";

ofstream ofile("file.txt");
ofile << str;
```

- `write()`: Used to write **binary** data.


```
ofile.write((char*)&data, numChars);
```

```
ofstream ofile("file.txt", ios_base::binary);
double a = 4.2442;
int b = 84;
char c[3] = {'a', 'b', 'c'};

ofile.write((char*)&a, sizeof(double));
ofile.write((char*)&b, sizeof(int;
ofile.write(c, 3);
```

```
void write(ostream &os)   // class member (stores temperature)
{
  os.write((char*)&min, sizeof(double));
  os.write((char*)&max, sizeof(double));
}
```

```
ostream ofile("file.txt", ios_base::binary);
myclass(1.4, 7.5).write(ofile);
myclass(4.3, 6.8).write(ofile);
```

- `stringstream` operations can help.

```
stringstream ss;
ss << name1 << age1 << '\n'
  << name2 << age 2 << "\n";

ofile << ss.str();
//ofile << ss.rdbuf();
//ofile << ss.c_str();
```

### Read (input)

For reading, use a loop to iterate over the records (`endl`). Use `eof()` to detect when you reached the end-of-file.

- `getline()`: Read an entire line of text from a file stream object. It returns false at the end-of-line.

```
ifstream ifile("file.txt");
string line;

while(getline(ifile, line))
  cout << line << endl;

ifile.close();
```

- `>>` operator: Read strings and formatted text data. You must know the order of tokens in the file (example: if the next token is a double, you must read it into a doble, or an error will occur). It skips whitespaces by default.

```
int a, b;
while(ifile >> a >> b)
  ...
```

- `read()`: Used for reading **binary** data. It takes a specified number of bytes and stores them into a variable. The next call will read the next bytes.

```
ofile.read((char*)&data, numChars);
```

```
ifstream ifile("file.txt", ios_base::binary);
double a;
int b;
char c[3];

ifile.read((char*)&a, sizeof(double));
ifile.read((char*)&b, sizeof(int));
ifile.read(c, 3);
```

```
void read(istream &is)   // class member (stores temperature)
{
  os.read((char*)&min, sizeof(double));
  os.read((char*)&max, sizeof(double));
}
```

```
istream ifile("file.txt", ios_base::binary);
while(!file.eof())
{
  myClass obj;
  obj.read(ifile);
  if(ifile.gcount() == 0)
    break;
  cout << obj.temperatures;   // << operator is overloaded
}
```

- `stringstream` operations can help.

```
while(getline(ifile, line))
{
  istringstream iss(line);
  int a, b;
  if(!(iss >> a >> b))
    break;
}
```

```
stringstream sstr;
sstr << ifile.rdbuf();
string str = sstr.str();
```

### Positioning

C++ stream objects keep track of the current read/write position in the stream.

- `istream` and `ifstream`:

  - `tellg()`: Obtain the current **get** position.
  - `seekg()`: Modify its position.

- `ostream` and `ofstream`:

  - `tellp()`: Obtain the current **put** position.
  - `seekp()`: Modify its position.

- `iostream` and `fstream`:

  - `tellg()` & `tellp()`: Obtain the current **get** and **put** positions.
  - `seekg()` & `seekp()`: Modify its position.

**tellg()** and **tellp()** return a **std::streampos** value.

**seekg()** and **seekp()** are overloaded methods (can take 1 or 2 parameters):

- `istream& seekg(streampos pos)`
- `ostream& seekp(streampos pos)`
- `istream& seekg(streamoff off, ios_base::seekdir way)`
- `ostream& seekp(streamoff off, ios_base::seekdir way)`

Parameters:

- `streamoff`: Specify a relative offset.
- `ios_base::seekdir`: Specify the offset direction.
  - `ios_base::beg`
  - `ios_base::cur`
  - `ios_base::end`
  - etc.

**Examples**:

```
void **write**(ostream &os, int index)
{
  streampos pos(index * RECORD_SIZE);
  os.seekp(pos);
  os.write((char*)&min, sizeof(double));
  os.write((char*)&max, sizeof(double));
}

int main()
{
  fstream ofile("file.txt", ios_base::binary | ios_base::out | ios_base::in);
  **write**(ofile, index);
  ofile.close();
}
```

```
void **read**(istream &is, int index)
{
  streampos pos(index * RECORD_SIZE);
  is.seekg(pos);
  is.read((char*)&min, sizeof(double));
  is.read((char*)&max, sizeof(double));
}

int main()
{
  fstream ifile("file.txt", ios_base::binary | ios_base::out | ios_base::in);
  **read**(ifile, index);
  ifile.close();
}
```


## String streams

**String stream**: Stream object that reads or writes a `string`. In addition to the normal iostream operations, string streams define an overloaded member called `str()`. Calling str with no arguments returns the string to which the string stream is attached. Calling it with a string attaches the string stream to a copy of that string.

The `<sstream>` header defines 3 types to support in-memory IO:

- `istringstream` type reads from a string (`>>`).
- `ostringstream` type writes to a string (`<<`).
- `stringstream` type read and writes a string (`>>` & `<<`).

```
ostringstream os1;
os1 << "Jane" << " " << 35 << " " << 12000 << endl;  // overrides existing content
os1.str("Jane 32 15000");
cout << os1.str();

ostringstream os2(myString);

ostringstream os3(ios_base::binary);
```

```
string name;
int age;
double salary;
istringstream is1(os1.str());
is1 >> name >> age >> salary;

istringstream is2(os3.str(), ios_base::binary);
```

These types inherit from the types we have used from the `iostream` header. They also add members to manage the string associated with the stream.

```
sstream strm;            // Unbound stringstream
sstream strm(s);         // Stringstream holding a copy of string s
strm.str();              // Returns a copy of the string that strm holds
strm.str(s);             // Copies string s into strm (returns void)
```

**istringstream**

Often used when we have some work to do on an entire line with individual words within it.

_Example_: We have a file where each line contains a name and a variable number of phone numbers.

```
struct PersonInfo {
    string name;
    vector≺string≻ phones;
}

string line, word;
vector≺PersonInfo≻ people;
while(getline(cin, line)) {
    PersonInfo info;
    istringstream record(line);
    record >> info.name;
    while(record >> word) info.phones.push_back(word);
    people.push_back(info);
}
```

The _inner while_ ends when we’ve read all the data in `line`. When the string has been completely read, EOF (end-of-file) is signaled and the next input operation fails. The _outer while_ continues until we hit EOF on cin.

**ostringstream**

Useful for output a little at a time, not printing the output until later.

_Example_: We want to validate and reformat the phone numbers, and then put them in a new file. If any person has any invalid numbers, we won’t put them in the new file. We won’t produce the output until we’ve seen and validated all the numbers from one person, so we will write the output to an in-memory `ostringstream`. Will assume the function `valid` and `format`.

```
for(const auto &entry : people) {
    ostringstream formatted, badNums;
    for(const auto &nums : entry.phones) 
    {
        if(!valid(nums)) badNums ≺≺ " " ≺≺ nums;
        else formatted ≺≺ " " ≺≺ format(nums);
    }
    if(badNums.str().empty()) os ≺≺ entry.name ≺≺ " " ≺≺ formatted.str() ≺≺ endl;
    else cerr ≺≺ "input error: " ≺≺ entry.name ≺≺ " invalid number(s) " ≺≺ badNums.str() ≺≺ endl;
}
```

**Extending strings to support custom classes**

You can easily define custom operator `>>` and operator `<<` functions to support stream input/output for custom classes (operator overloading).

```
class myClass {
    int x, y;
};

std::istream & operator >> (std::istream & is, myClass & obj) {
    is >> obj.x >> obj.y;
    return is;
}

std::ostream & operator << (std::ostream & os, const myClass & obj) {
    os << "[" << obj.x "," << obj.y <<"]";
    return os;
}
```

```
myClass obj1, obj2;
std::cin >> obj1 >> obj2;
std << obj1;
```

**Wide characters**

The `std::wchar_t` represents wide characters (non-roman character sets). There's a set of related classes and objects:

- `wstring`: String of wide characters.
- `wstream`, `wistream`, `wostream`: They allow to input (`wcin`) and output (`wcout`) wide characters.
- `wstringstream`, `wistringstream`, `wostringstream`: They allow to input and output wide characters to/from a string (stringstream).

```
wstringstream s;
s << "Jane" << " " << 42 << " " << 15000 << endl;
wstring formattedString = s.str();
wcout << formattedString;
```






