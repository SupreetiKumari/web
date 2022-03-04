 # Acknowledgements-

 http://rogerprice.org/ug/ug.pdf - From this pdf I have taken the entire pi file which consisted of - glue.sml, pi.lex, datatype.sml, compiler.sml, pi.yacc
 pi.cm . Then I have changed the lookahead in the compiler.sml. The glue.sml basically glues everything to that all the files are linked together. The 
 compiler.sml is used to print the parse tree . I have changed the datatype.sml to while_ast.sml. while_ast.sml is the file that is used to convert the parse tree 
 to abstract syntax tree. pi.lex is used to specify the terminals names. In pi.yacc we have provided the grammar according to the ebnf in the pl.pdf of the while 
 programming language. 
 
 https://github.com/arch1902/COL226-PL-Assignments - From this , I have referred assignment 2 and 3 from this github repo. From assignment 2 , I have used the 
 syntax of the yacc file . In the bracket part , I have used the format he has used. From his assignment 3, I have used his ast.sml file to make my while_ast.sml 
 file. I have used the way he has defined the the datatype binop. I have also used the way he has made his lex file.
 
 https://github.com/cinnabar233/Lexer-and-Parser-of-Boolean-Programs - I have also referred to his program , although not copied anything specifically.
 
 # AST DATATYPE-
 
 ## We can see the grammar from the yacc file-
 
 ### The terminals are-
 NUM | PLUS | MINUS | TIMES | LPAREN | RPAREN | RBRACES | LBRACES | ID | DIV | MOD | LT | LEQ | EQ | GT | GEQ | NEQ | INT | BOOL | VAR | SET | READ | WRITE | 
 IF | THEN | ELSE | ENDIF | WHILE | DO | ENDWH | NEG | OR | AND | TT | FF | NOT | PROG | SEQ | COLON | SEMICOLON | COMMA | EOF| TERM
 
 ### The non terminals are -
 START of string |Program of string | Block of string| DeclarationSeq of string| Declaration of string| Type of string| VariableList of string| CommandSeq of string|
 Command of string| CommandSeqUser of string | Expression of string|  Variable of string
 
 ## The production rules:
 
 Program ::= PROG ID SEQ Block
 
Block ::= DeclarationSeq CommandSeq .

DeclarationSeq ::= Declaration DeclarationSeq | Declaration

Declaration ::= VAR VariableList COLON Type SEMICOLON 
                

Type ::= INT | BOOL.

VariableList ::= Variable SEMICOLON VariableList | Variable

CommandSeq:LBRACES CommandSeqUser RBRACES

Command ::= Variable SET Expression | 

READ Variable |

WRITE Expression |

IF Expression THEN CommandSeq ELSE CommandSeq ENDIF |

WHILE Expression DO CommandSeq ENDWH.

CommandSeqUser: Command SEMICOLON CommandSeqUser | Command SEMICOLON

 Expression ::= IntExpression AddOp IntT erm | IntTerm  | BoolExpression “||” BoolTerm | BoolTerm .
 


IntTerm ::= IntTerm MultOp IntFactor | IntFactor .

IntFactor ::= Numeral | Variable |
“(”IntExpression“)” | “˜”IntFactor .


BoolTerm ::= BoolTerm “&&” BoolFactor | BoolF actor .

BoolFactor ::= “tt” | “ff” | V ariable | Comparison |
“(”BoolExpression“)” | “!”BoolF actor .

Comparison ::= IntExpression RelOp IntExpression .

Variable ::= Identifier .

RelOp ::= “<” | “<=” | “=” | “>” | “>=” | “<>” .

AddOp ::= “+” | “−” .

MultOp ::= “∗” | “/” | “%” .

Identifier ::= Letter{Letter | Digit} .

Numeral ::= [“˜”]Digit{Digit} .
 
 
 
 
 # Other design decisions-
 
 To make my grammar unambigious and  after seeing the dsig files generated I have changed the grammar in such a  such that it  does not give any conflicts of any 
 type. Hence I have combined the IntExpressions and BoolExpressions together to give a non ambigious grammar.
 
 # Other Implementation decisions-
 
 I have put the precedence operators to and defined another non terminal called CommandSeqUser to make to simpler. 
 
 # Auxillary Functions and Datatypes
 
 I have defined auxillary functions and variables in while_ast.sml -DEC, CMD etc.
 
 # RUN the file
 
 ml-lex ast.lex
 ml-yacc ast.yacc
 sml while_ast.sml
 sml compiler.sml
 

