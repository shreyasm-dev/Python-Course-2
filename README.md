# Python
We will be building our own programming language on top of Python. There are two types of programming languages:
- Compiled
	- This means that the computer looks at some code, and then gives the user code in **bytecode**, which the user has to run again.
		- *Bytecode*: Binary instructions that the computer can understand *directly*
- Interpreted
	- The computer looks at the code and keeps running code in a different programming language as it goes.

The programming language we will be making is going to be an *interpreted* language in Python. Python is interpreted, but the main version (CPython) is built on top of the programming language C, which is compiled.

## How an Interpreter works
We've talked about programming languages, but not about how they work. These are the steps:
1. Lexer (Lexical Analyzer, or Tokenizer)
2. Parser (Code validator)
3. Code generation (Run the code)
### The Lexer
A lexer
