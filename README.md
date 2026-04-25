### Overview

Aurora Compiler Suite is a three-phase compiler system built for a custom programming language. It simulates how modern compilers process source code step by step, starting from raw text and ending in optimized low-level output.

The system is divided into three major components:

* Frontend (Lexical, Syntax, and Semantic Analysis)
* Middle-End (Intermediate Representation and Optimization)
* Backend (Code Generation and Linking)

It is designed to demonstrate full compiler pipeline behavior in a structured and modular way, without skipping the painful details real compilers actually deal with.

---

## Project Goal

The objective of this system is to take a user-defined programming language and process it into executable-style output through a complete compilation pipeline.

Instead of treating compilation as a black box, this project opens it up step by step so every stage is visible, understandable, and (occasionally) unforgiving when errors appear.

---

# FRONTEND MODULE (Language Processing Core)

## Objective

The frontend is responsible for analyzing raw source code and ensuring it is valid according to the language rules before any deeper processing is done.

It acts like a strict gatekeeper: if your code is messy, it will not hesitate to reject it.

---

## Language Features Supported

The custom language includes:

* Data types: int, float, bool
* Variables and assignments
* Arithmetic and logical expressions
* Control structures:

  * if-else
  * while loops
  * for loops
  * switch-case
* Functions with parameters and return types
* Recursion support
* Basic input/output operations
* Operators:

  * Arithmetic (+, -, *, /, %)
  * Logical (&&, ||, !)
  * Relational (==, !=, <, >, <=, >=)

---

## Frontend Components

### 1. Lexical Analysis

This stage converts raw code into tokens.

Responsibilities:

* Token generation (keywords, identifiers, operators, literals)
* Handling whitespace and comments
* Detecting invalid tokens
* Reporting lexical errors with line numbers

Output:

* Stream of tokens with metadata

At this stage, the program is basically asking:
“Are you even writing real code or just typing random symbols?”

---

### 2. Syntax Analysis

This stage validates grammatical structure using a defined grammar.

Responsibilities:

* Parsing token stream
* Constructing Abstract Syntax Tree (AST)
* Validating control structures and expressions
* Reporting syntax errors clearly

Output:

* AST representation of the program

If lexical analysis checks vocabulary, syntax analysis checks whether your sentences actually make sense.

---

### 3. Semantic Analysis

This stage ensures the program is logically correct.

Responsibilities:

* Symbol table creation (variables, functions, scope tracking)
* Type checking (e.g., preventing int + bool nonsense)
* Detecting undeclared variables
* Validating function calls and return types
* Scope validation

Output:

* Semantic error reports with detailed explanations

This is where the compiler stops being polite and starts pointing out logical mistakes.

---

# MIDDLE-END MODULE (Optimization Layer)

## Objective

The middle-end transforms the validated AST into an Intermediate Representation (IR) and applies optimizations to improve efficiency before final code generation.

---

## Responsibilities

### 1. Intermediate Representation (IR) Generation

* Converts AST into a simplified low-level structure
* Makes code easier to optimize and analyze

---

### 2. Code Optimization

Includes:

* Constant folding
* Dead code elimination
* Expression simplification
* Redundant computation removal

---

## Output

* Optimized IR ready for backend processing

At this stage, the compiler stops caring about how your code looks and starts caring about how inefficient it is.

---

# BACKEND MODULE (Code Generation Engine)

## Objective

The backend converts optimized intermediate representation into low-level target code.

---

## Responsibilities

### 1. Code Generation

* Translates IR into assembly-like or machine-style instructions
* Maps variables to memory locations
* Converts expressions into executable operations

---

### 2. Linking and Final Output

* Combines generated instructions into final program output
* Prepares execution-ready code structure

---

## Output

* Final generated code representing the original program

This is where everything either comes together nicely or falls apart depending on how well earlier stages behaved.

---

# SYSTEM FLOW OVERVIEW

1. Source code is written in the custom language
2. Lexical analysis converts it into tokens
3. Syntax analysis builds AST
4. Semantic analysis validates logic and builds symbol table
5. IR is generated in middle-end
6. Optimizations are applied
7. Backend generates final code
8. Output is produced

---

# DESIGN HIGHLIGHTS

* Fully modular compiler pipeline
* Separation of frontend, middle-end, and backend
* Structured error reporting at every stage
* AST-based syntax representation
* Symbol table with scope management
* IR-based optimization layer
* Scalable design for future language expansion

---

# FILE STRUCTURE

The project is organized into multiple source files representing each compiler stage:

* Frontend modules (lexer, parser, semantic analyzer)
* Middle-end modules (IR generator, optimizer)
* Backend modules (code generator, linker)

Each file handles a specific responsibility, ensuring clean separation of concerns instead of one giant chaotic file pretending to be a compiler.

---

# CHALLENGES FACED

* Designing grammar for a custom language
* Handling nested scopes in symbol table
* Ensuring correct AST generation for complex expressions
* Managing IR consistency across transformations
* Debugging silent semantic errors that looked “fine” but were absolutely not fine

---

# IMPROVEMENTS (Future Scope)

* Add GUI-based AST visualization
* Expand language features (classes, objects, inheritance)
* Improve optimizer with advanced techniques (loop unrolling, SSA form)
* Add real executable backend targeting actual assembly
* Support multiple target architectures

---

# CONCLUSION

Aurora Compiler Suite demonstrates a complete compiler pipeline from raw source code to optimized output. It brings together lexical analysis, parsing, semantic validation, optimization, and code generation into a unified system.

In simple terms, it takes code that *looks right*, checks if it *is right*, optimizes it so it runs better, and then translates it into something a machine can actually understand.

And if the input is wrong, it doesn’t hesitate to tell you exactly where you messed up — sometimes more clearly than a human reviewer would.
