# parsel-ql

A simple parser for sql written in python. I needed a sql-parser for a
different project. I found some implementation using pyparsing but none
of them were able to parse some complex arithmetic expressions. So I decided
to implemented by myself.

## Boolean and Arithmetic expression in parsel-sql

Implementing a sql-parser with pyparsing is not as simple as people think.
The most difficult part was the grammar for the boolean and arithmetic
expressions. The example in pyparsing-site use a criptic method called:
"operatorPrecedence" to build the expression and it's extremely slow.
Hopefully, I found Crenshaw's tutorial [1] (How to write a compiler) and
I implemented my expressions following his suggestions. Here the grammar:

      <b-expression> ::= <b-term> [<orop> <b-term>]*
      <b-term>       ::= <not-factor> [AND <not-factor>]*
      <not-factor>   ::= [NOT] <b-factor>
      <b-factor>     ::= <b-literal> | <b-variable> | <relation>
      <relation>     ::= | <expression> [<relop> <expression]
      <expression>   ::= <term> [<addop> <term>]*
      <term>         ::= <signed factor> [<mulop> factor]*
      <signed factor>::= [<addop>] <factor>
      <factor>       ::= <integer> | <variable> | (<b-expression>)

[1] http://compilers.iecc.com/crenshaw/tutor6.txt

Author
------
parsel-ql is developed and probably not maintained by Harold Valdivia-Garcia

