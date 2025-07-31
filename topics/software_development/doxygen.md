# Doxygen

## Table of Contents
+ [Installation](#installation)
+ [Getting started](#getting-started)
+ [Documenting the code](#documenting-the-code)
+ [My system](#my-system)
+ [LSST style](#lsst-style)
  + [Boilerplate](#boilerplate)
  + [Basic format of documentation blocks](#basic-format-of-documentation-blocks)
  + [Common structure of documentation blocks](#common-structure-of-documentation-blocks)
+ [References](#references)


## Installation

[Installation](https://www.doxygen.nl/manual/install.html): From source or binaries, in Windows or Unix.

[GIT repository](https://github.com/doxygen/doxygen)

### Unix

- Required: flex, bison, libiconv, GNU make, CMake, Python.
- For nicer diagrams: GraphViz (set HAVE_DOT to yes)
- For PDF output: a LaTeX distribution (like [TeX Live](https://www.tug.org/interest.html#free))

```
git clone https://github.com/doxygen/doxygen.git
sudo apt-get install flex
sudo apt-get install bison
```

```
cd doxygen
mkdir build
cd build
cmake -G "Unix Makefiles" ..
make
sudo make install
```

### Windows

- Download **Doxygen** installer and install it easily. Set path as environment variable.
- For nicer diagrams, download **GraphViz** installer and install it (set HAVE_DOT to yes). Set path as environment variable.
- For PDF output: a **LaTeX** distribution (like [MikTex](https://miktex.org/) or [proTeXt](https://www.tug.org/protext/)) and [**Ghostscript**](https://sourceforge.net/projects/ghostscript/).


## Getting started

The executable **doxygen** is the program that parses the sources and generates documentation. The graphical environment is **doxywizard**. Below you can see the tools and the flow of information between them:

<br>![information_flow](https://raw.githubusercontent.com/AnselmoGPP/know_base/master/topics/software_development/resources/infoflow.png)

By default, Doxygen supports C, C++, C#, Objective-C, IDL, JAVA, VHDL, PHP, Python, Fortran, D.

**First steps:**

- Create a configuration file
- Run doxygen
- Document the sources

### Configuration file

Each project should have its own configuration file. For simplification, doxygen can create a template configuration file with:

```
doxygen -g <config_file>
```

- `config_file`: name of the configuration file

This file’s format is similar to that of a simple Makefile. It contains a number of assignemnts (tags) like:

```
TAGNAME = VALUE1
```

```
TAGNAME = VALUE1 VALUE2 …
```

You can probably leave the values of most tags with its default values. You can edit it with a text editor, or use *doxywizard*, which lets you create, read and write doxygen configuration files, and set configuration options.

If you leave `INPUT` tag empty, doxygen will search for sources in the current directory. Or you can assign the root directory/directories to it, and add one or more file patterns to the `FILE_PATTERNS` tag (*.cpp, *.h…) (if omitted, a list of typical patterns is used).

`RECURSIVE` set to `YES`: recursive parsing a source tree

`EXCLUDE` and `EXCLUDE_PATTERNS` tags can be used.

```
EXCLUDE_PATTERNS = */test/*       <- omit all test directories from a source tree
```

Doxygen looks at the file’s extension (.cpp, .h, .txt, …) to determine how to parse a file. To include wildcard extensions, add them to ``FILE_PATTERNS` and set the appropriate `EXTENSION_MAPPING`.

`EXTRACT_ALL` set to `YES`: doxygen will pretend everything in your sources is documented (won’t generate warnings about undocumented member).

`SOURCE_BROWSER` set to `YES`: doxygen will generate cross-reference a (documented) entity with its definition in the source files.

`INLINE_SOURCES` set to `YES`: Include the sources directly into the documentation.

**My favorite options**:

- `PROJECT_NAME = "project name"`
- `PROJECT_BRIEF = "brief description here"`
- `INPUT = include`
- `RECURSIVE = YES`
- `EXTRACT_ALL = NO`
- `EXTRACT_PRIVATE = YES`
- `SOURCE_BROWSER = YES`
- `OUTPUT_DIRECTORY = XXX`

### Running doxygen

```
doxygen <config_file>
```

This creates, inside the output directory, one or more directories containing the generated documentation in one or more formats (HTML, RTF, LaTeX, XML, Unix-Man page, DocBook format).

`OUTPUT_DIRECTORY`: Set the output directory (by default, it is where doxygen is started).

Specify format: `HTML_OUTPUT`, `RTF_OUTPUT`, `LATEX_OUTPUT`, `XML_OUTPUT`, `MAN_OUTPUT`, `DOCBOOK_OUTPUT`.

### Documenting the sources

`EXTRACT_ALL` set to `NO` (default): doxygen will only generate documentation for documented entities.

Ways of documenting **members**, **classes** and **namespaces**:

- Place a special documentation block in front (or behind) of the declaration or definition
- Place a special documentation block with a structural command (it links the block with an entity that can be documented) somewhere else (another file or location). Files can only be documented this way.


## Documenting the code

### Special comment blocks

Special C++ style comment block with additional markings that let doxygen identify it as structured text that need to end up in the generated document.

For each entity in the code there are 2 or 3 types of **descriptions**, which together form the documentation for that entity:

- **Brief** description: Short one-liner. Also used in the HTML output for providing tooltips for references.
- **Detailed** description: Longer, more detailed.
- **Body** description (for methods and functions): Concatenation of all comment blocks found within the body.

**Detailed descriptions** (doxygen ommits intermediate `*`):

```
/**
    ... text ...
 */
```

```
/*!
    ... text ...
 */
```

```
///
/// ...text ...
///
```

```
//!
//! ...text ...
//!
```

```
/********************************************//**
 *  ... text
 ***********************************************/
```

If `JAVADO_BANNER = YES`:

```
/************************************************
 *  ... text
 ***********************************************/
```

```
/////////////////////////////////////////////////
/// ... text ...
/////////////////////////////////////////////////
```

**Brief descriptions**:

Three options:

- Use `/brief` with one of the above comments. Brief description ends with an empty line.

```
/*! \brief Brief description.
 *         Brief description continued.
 *
 *  Detailed description starts here.
 */
```

- If `JAVADOC_AUTOBRIEF = YES`, when using javadoc style comment blocks or multi-line special C++ comments will start automatically with a brief description which ends at the first dot followed by a space or new line.

```
/** Brief description which ends at this dot. Details follow
 *  here.
 */
```

```
/// Brief description which ends at this dot. Details follow
/// here.
```

- Use a special C++ style comment which doesn’t span more than one line.

```
/// Brief description.
/** Detailed description. */
```

```
//! Brief description.

//! Detailed description 
//! starts here.
```

The blank line is required to separate the brief description from the detail description. `JAVADOC_AUTOBRIEF` should be set to `NO`.

If you have multiple detailed descriptions, they will be joined. Even when they are at different places in the code.

```
//! Brief description, which is
//! really a detailed description since it spans multiple lines.
/*! Another detailed description!
 */
```

Documentation of member (including global functions) can be put in front of their definition. You could put the brief description before the declaration (header file) and the detailed description before the member definition (source file).

**Documentation after members**

Use an additional `<` marker to document after **member** (of a file, struct, union, class, or enum) or **parameters**.

```
int var; //!< Brief description after the member
```

```
int var; ///< Brief description after the member
```

```
int var; /**< Detailed description */
```

```
int var; /*!< Detailed description */
```

```
int var; //!< Detailed description
         //!< 
```

```
int var; ///< Detailed description
         ///<
```

For functions, you can use the `@param` command to document the parameters and then use `[in]`, `[out]`, `[in,out]` to document the direction. Some useful commands: `@param`, `@return`, `@see`, …

For inline documentation, it’s possible this:

```
void foo(int v /**< [in] docs for input parameter v */);
```

**Examples**:

```
 //! A normal member taking two arguments and returning an integer value.
 /*!
   \param a an integer argument.
   \param s a constant character pointer.
   \return The test results
   \sa QTstyle_Test(), ~QTstyle_Test(), testMeToo() and publicVar()
 */
int testMe(int a,const char *s);
```

```
 //! An enum.
 /*! More detailed enum description. */
enum TEnum {
             TVal1, /*!< Enum value TVal1. */
             TVal2, /*!< Enum value TVal2. */
             TVal3 /*!< Enum value TVal3. */
           }
```

```
 //! Enum variable.
 /*! Details. */
enumVar;
```

Examples: [link](https://www.doxygen.nl/manual/docblocks.html)

`BRIEF_MEMBER_DESC` set to `NO`: Brief descriptions doesn’t appear in the member overview of a class/namespace/file.

`REPEAT_BRIEF` set to `NO`: Brief descriptions won’t become the first sentence of the detailed description (by default they are).

`JAVADOC_AUTOBRIEF` set to `YES`: The first sentence of the documentation block is automatically treated as a brief description. If enabled, if you want to put a point without ending the sentence, you should put `\`  after it.

```
/** Brief description (e.g.\ using only a few words). Details follow. */
```

**Documentation at other places**

You can put documentation somewhere else, not just before/after the declaration/definition, by using structural commands. This is required for documenting files. Doxygen allows to put documentation blocks anywhere (except a body of a function, or inside normal C-style comment blocks).

Doxygen commands start with a backslash `\` or a `@` (Javadoc style), followed by a command name and one or more parameters

```
/*! \class Test
    \brief A test class.

    A more detailed class description.
*/
```

Some **structural commands**:

- `\class`
- `\union`
- `\enum`
- `\fn`: function
- `\var`: variable/typedef/enum value
- `\def`: #define
- `\typedef`
- `\file`
- `\namespace`
- `\package`: Java package
- `\interface`: IDL interface

To document a member of C++ *class**, you must also document the class itself. The same for **namespaces**. To document global objects (function, typedef, enum or preprocessor) definition you must must document the file that contains it (usually, a header file). Example: there must at least be this line in the file:

```
/** @file */
```

```
/*! \file */
```

Because these comment blocks contain a structural command, they can be moved to another location or input file, without affecting the generated documentation. But prototypes are duplicated, so all changes have to be made twice. You should avoid structural commands when possible.

```
/*! \file structcmd.h
 \brief A Documented file.

 Details.
*/

/*! \def MAX(a,b)
 \brief A macro that returns the maximum of \a a and \a b.

 Details.
*/

/*! \fn int open(const char *pathname,int flags)
 \brief Opens a file descriptor.

 \param pathname The name of the descriptor.
 \param flags Opening flags.
*/
```

If you put a comment block in a `.dox`, `.txt` or `.doc` file, doxygen will hide this file from the file list.

If you have a file that doxygen cannot parse but still would like to document it, you can show it as-is using `\verbinclude`.

```
/*! \file myscript.sh
 *  Look at this nice script:
 *  \verbinclude myscript.sh
 */
```

The script has to be explicitly listed in `INPUT`, or `FILE_PATTERNS` has to include the `.sh` extension, and the script has to be found in the path set via `EXAMPLE_PATH`.

**Comment formatting**

Doxygen supports various styles of formatting your comments:

- Plain text
- Markdown syntax (including parts of the Markdown Extra extension) ([link](https://www.doxygen.nl/manual/markdown.html))
- Javadoc like markup ([link](https://www.doxygen.nl/manual/commands.html))
- XML markup (as specified in the C# standard) ([link](https://www.doxygen.nl/manual/xmlcmds.html))


## My system

There are 3 types of descriptions: Brief, Detailed, Body. You could put the brief description before the declaration (header file) and the detailed description before the member definition (source file).

- **Member variable**:

```
int member;    //!< Description here
```

- **Method**:

```
/**
    @brief Brief description. 

    Detail description. Maybe put a list:
    <ul>
        <li>hello world</li>
        <li>hello doxygen</li>
    @param name1 Description here
    @param name2 Description here
    @return name2 Description here
*/
```

- **Class**:

```
/** 
    @class Test 
    @brief A test class. 

    A more detailed class description.
*/
```

- **Function**:

```
/*! 
    @fn int open(const char *pathname,int flags)  
    @brief Opens a file descriptor.  
    @param pathname The name of the descriptor.  
    @param flags Opening flags.  
    @return The test results 
*/
```

- **Macro**:

```
/*!
    @def MAX(a,b)
    @brief A macro that returns the maximum of \a a and \a b.

    Details.
*/
```

- **Others**:

```
/// Brief description that works well when put before some object (method, class, variable).
```

```
/// Brief description which ends at this dot. Details follow 
/// here.
```

```
/// Brief description. 
/** Detailed description. */
```

```
int var; ///< Brief description after the member 
int var; /**< Detailed description */
```

Some **structural** commands (may use `\` or `@`): `\class`, `\union`, `\enum`, `\fn` (function), `\var` (variable/typedef/enum value), `\def` (#define), `\typedef`, `\file`, `\namespace`, `\package` (Java package), `\interface` (IDL interface).


## LSST style

**LSST**: Large Synoptic Survey Telescope

### Boilerplate

For header (`.h`) and source (`.cc`) files:

- Formatting hint for Emacs

```
// -*- lsst-c++ -*-
```

- Copyright and license block

Ordinary C++ comments may be used to document files for developers reading the source code.

### Basic format of documentation blocks

- **Multi-line** documentation blocks: `/**` … `*/`
- **Single-line** documentation: `///` (some special cases use ///<)
- For consistency, don’t begin documentation blocks with `/*!` or `//!`

Multi-line documentation delimiters (`/**`, `*/`) should be on their own lines.

Use Javadoc-style **tags** (`@see`, `@param`, `@return`, …).

Use **Markdown-formatted Doxygen comment blocks** for formatting. If some format cannot be expressed with Markdown, you may use **Doxygen’s built-in formatting** or **HTML markup**.

Documentation must appear where a component is first declared (therefore, in header files).

Documentation must appear before the declaration it describes, and with the same indentation.

```
/**
 * Sum numbers in a vector.
 *
 * @param values Container whose values are summed.
 * @return sum of `values`, or 0.0 if `values` is empty.
 */
double sum(std::vector<double> & const values) {
    ...
}
```

### Common structure of documentation blocks

1. [Short Summary](https://developer.lsst.io/cpp/api-docs.html#cpp-doxygen-short-summary)
2. [Extended Summary](https://developer.lsst.io/cpp/api-docs.html#cpp-doxygen-extended-summary) (recommended)
3. [Template Parameters](https://developer.lsst.io/cpp/api-docs.html#cpp-doxygen-tparameters) (if applicable; for classes, methods, and functions)
4. [Function/Method Parameters](https://developer.lsst.io/cpp/api-docs.html#cpp-doxygen-parameters) (if applicable; for methods and functions)
5. [Returns](https://developer.lsst.io/cpp/api-docs.html#cpp-doxygen-returns) (if applicable; for methods and functions)
6. [Throws](https://developer.lsst.io/cpp/api-docs.html#cpp-doxygen-throws) (if applicable; for methods and functions)
7. [Exception Safety](https://developer.lsst.io/cpp/api-docs.html#cpp-doxygen-exceptsafe) (optional; for methods and functions)
8. [Helper Functions](https://developer.lsst.io/cpp/api-docs.html#cpp-doxygen-related) (if applicable; for functions)
9. [Initializer Declaration](https://developer.lsst.io/cpp/api-docs.html#cpp-doxygen-initializer) (optional; for constants)
10. [See Also](https://developer.lsst.io/cpp/api-docs.html#cpp-doxygen-see-also) (optional)
11. [Notes](https://developer.lsst.io/cpp/api-docs.html#cpp-doxygen-notes) (optional)
12. [References](https://developer.lsst.io/cpp/api-docs.html#cpp-doxygen-references) (optional)
13. [Examples](https://developer.lsst.io/cpp/api-docs.html#cpp-doxygen-examples) (optional)


## References

- [Doxygen manual](https://www.doxygen.nl/manual/)
- [Documenting C++ code](https://developer.lsst.io/cpp/api-docs.html)
- [How to document C++](http://www.edparrish.net/common/cppdoc.html)
