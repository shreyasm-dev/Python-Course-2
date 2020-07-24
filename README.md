# Python
We will be building our own programming language on top of Python. Knowing how to build a programming language and knowing how programming languages work are two very important skills that will be ***very*** important in the future. And learning how to build one can also be fun and make you a lot better at Python.

 There are two types of programming languages:
- Compiled
	- This means that the computer looks at some code, and then gives the user code in **bytecode**, which the user has to run again.
		- *Bytecode*: Binary instructions that the computer can understand *directly*
- Interpreted
	- The computer looks at the code and keeps running code in a different programming language as it goes.

The programming language we will be making is going to be an *compiled* language which is written in Python. It will be called "*Archários*", which is Greek for "beginner". Python is interpreted, but the main version ([CPython](https://github.com/python/cpython)) is built on top of the programming language C, which is compiled.

## Archários
Archários code looks a little like Python code. You use `out()` to print out  something (it works exactly the same as `print()` in Python), and you can do math like you can do in Python. To get input, instead of `input()` like you would use in Python, in Archários, you use `in()`.

## Building the programming language
These are the three steps that a programming language has to do:
1. Lexer (Lexical Analyzer, or Tokenizer)
2. Parser (Abstract syntax tree generator)
3. Code generation (Run the code)

### The Lexer
A lexer takes code and breaks it up into pieces (also called tokens or lexemes). So for example, if we inputted the code `myVariable = 999`, the lexer would give the parser input (a list), and the parser would output something like this:
```javascript
[{
  lexeme: "myVariable",
  type: Tokens.IDENTIFIER
}, {
  lexeme: "=",
  type: Tokens.EQUALS
}, {
  lexeme: "999",
  type: Tokens.NUMBER
}]
```

We get a list of objects. Each object has `lexeme` and `type` properties. The `lexeme` is the literal value of the item. `type` is the type of the item. A lexeme is a token produced by the lexer. It can be complicated to write a lexer on our own, so we will be using a Python module called `rply`. `rply` is a lexer generator, which means that we have to write some code, and it will create a lexer for us! First, we need to import `rply`, so create a file called `lexer.py`, and put in this code:
```python
from rply import LexerGenerator
```
What it does is imports something called "`LexerGenerator`" from the module "`rply`". Now we can use `LexerGenerator` later in the code. We need to store `LexerGenerator` somewhere to modify it and add things to it. We can use a variable called `lexer`.
```python
lexer = LexerGenerator()
```
The above code will create a new lexer so we can use it. Now, we need to add "tokens" to the lexer, so the lexer actually knows how to separate the tokens. To add a token, we will do something like this:
```python
lexer.add("TOKEN_NAME", r"TOKEN_REGEX")
```
`"TOKEN_NAME"` is the name of the token that will be used in the parser later. The `r` behind `"TOKEN_REGEX"` means that we will not have to escape anything inside the string, so instead of `"\\"` (which translates to `"\"`), we can just do `r"\"` (which *still* translates to `"\"`). If we had `"\"` (without the `r`) Python would give us an error. The second string has to be a *Regular Expression* (regex/ regexp for short). It is a way in a lot of programming languages to match an item in a string without manually writing a function to get the value. You can find a simple tutorial on regular expressions [here]([https://www.w3schools.com/python/pyton_regex.asp). Sometimes, we still have to escape characters inside the regular expression because they mean something special in regular expressions. 

Our first token will be the `out()` function. In Python, you can do this:
```python
def hello():
	print("Hello")

x = hello

x()
```
This will print `hello` to the screen because you can actually access the function using just the name of the function, instead of using it with `(` and `)`. Archários is like Python. We can access `out` by using `out` or `out()`. So the lexer will actually match `out` instead of `out()`. The regex for this will just be "out".  Create a function called `addTokens` and put the code `lexer.add("OUT", r"out")` inside it. `"OUT"` is the type of the token, and `r"out"` is the thing that the lexer should *actually* match.
```python
def addTokens():
	lexer.add("OUT", r"out")
```
Add this at the end of the file:
```python
def get_lexer():
	add_tokens()
	return lexer.build()
```
This is just a function that adds the tokens by running `addTokens()` and it runs `lexer.build()` which is a function that `rply` (the Python lexer generator we're using) uses to finish the lexer. We will not need to edit this function at all. Add this code in a new file called `main.py`:
```python
import lexer # Import the file

text_input =  "out"  # This is the input
lexer = lexer.get_lexer()  # Get the lexer
tokens = lexer.lex(text_input)  # Tokenize the input

for token in tokens:
	print(token)  # Print out the input
```
That code was just some code that we will use for testing. It *will* be changed later.
