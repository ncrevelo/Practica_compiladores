
# Practica1 
# Comandos utilizados: 
antlr4 Calculadora.g4 javac *.java
java org.antlr.v4.runtime.misc.TestRig Calculadora prog -tokens < input.txt
java org.antlr.v4.runtime.misc.TestRig Calculadora prog -tree < input.txt
# Expresion generada para los tokens echo -e "a = 10;\nb = 5 + a * 2;\nc = (b - 3) / 2;" | java org.antlr.v4.runtime.misc.TestRig Calculadora prog -tokens
# Tokens generados: 
[@0,0:0='a',<ID>,1:0]
[@1,2:2='=',<'='>,1:2]
[@2,4:5='10',<INT>,1:4]
[@3,6:6=';',<';'>,1:6]
[@4,8:8='b',<ID>,2:0]
[@5,10:10='=',<'='>,2:2]
[@6,12:12='5',<INT>,2:4]
[@7,14:14='+',<'+'>,2:6]
[@8,16:16='a',<ID>,2:8]
[@9,18:18='',<''>,2:10]
[@10,20:20='2',<INT>,2:12]
[@11,21:21=';',<';'>,2:13]
[@12,23:23='c',<ID>,3:0]
[@13,25:25='=',<'='>,3:2]
[@14,27:27='(',<'('>,3:4]
[@15,28:28='b',<ID>,3:5]
[@16,30:30='-',<'-'>,3:7]
[@17,32:32='3',<INT>,3:9]
[@18,33:33=')',<')'>,3:10]
[@19,35:35='/',<'/'>,3:12]
[@20,37:37='2',<INT>,3:14]
[@21,38:38=';',<';'>,3:15]
[@22,40:39='<EOF>',<EOF>,4:0]
 # árbol de análisis sintáctico: 
 (-tree) Expresion: echo -e "a = 10;\nb = 5 + a * 2;\nc = (b - 3) / 2;" | java org.antlr.v4.runtime.misc.TestRig Calculadora -tree
# Expresion generada:
(prog (stat (assignStmt a = (expr 10) ;)) (stat (assignStmt b = (expr (expr 5) + (expr (expr a) * (expr 2))) ;)) (stat (assignStmt c = (expr (expr ( (expr (expr b) - (expr 3)) )) / (expr 2)) ;)))
# 1. ¿Cómo se representan los operadores +, -, * y / en los tokens generados?
R/ Se definen Como operadores aritméticos específicos, por lo que quiere decir que ANTLR4 si reconoce estos operadores como tokens individuales, pero no los define explícitamente en las reglas léxicas ejemplo luxer
Estos estan definidos por la regla sintáctica:
expr: expr ('*'|'/') expr 
    | expr ('+'|'-') expr 
    | '(' expr ')'
    | ID
    | INT;
Tokens individuales en la salida de ANTLR4 (ejemplo: [@7,14:14='+',<'+'>,2:6]).

# 2. ¿Qué estructura sigue el árbol de análisis sintáctico generado por ANTLR4 para la expresión b = 5 + a * 2;?
R/ * se evalúa antes que +, organizando el árbol en función de la precedencia.
En esta gramática, cuando vemos 'a * 2', se debe calcular primero, antes de la suma con el 5
 Respuesta correcta: d) * se evalúa antes que +, organizando el árbol en función de la precedencia, en la salida de -tree, el árbol generado muestra b = (5 + (a * 2)), respetando la precedencia.

# 3. ¿Por qué es importante visualizar los tokens y el árbol de análisis en el proceso de compilación?
Respuesta correcta: d) Todas las anteriores.

son todas las anteriores ya que Analiza los tokens y el árbol ayuda a comprender cómo el código fuente se descompone en estructuras y la estructura del árbol influye en la generación de código y permite detectar errores en la gramática y corregir problemas.


# Practica 2 
Comandos utilizados 
# Comandos utilizados: 
antlr4 Calculadora.g4 javac *.java
java org.antlr.v4.runtime.misc.TestRig Calculadora prog -tokens < input.txt
java org.antlr.v4.runtime.misc.TestRig Calculadora prog -tree < input.txt
# Expresion generada para los tokens 
echo -e "x = 0;\nwhile (x < 5) {\n    x = x + 1;\n}" | java org.antlr.v4.runtime.misc.TestRig MiGramatica programa -tokens
# Tokens generados: 
[@0,0:0='x',<ID>,1:0]
[@1,2:2='=',<'='>,1:2]
[@2,4:4='0',<INT>,1:4]
[@3,5:5=';',<';'>,1:5]
[@4,7:11='while',<'while'>,2:0]
[@5,13:13='(',<'('>,2:6]
[@6,14:14='x',<ID>,2:7]
[@7,16:16='<',<'<'>,2:9]
[@8,18:18='5',<INT>,2:11]
[@9,19:19=')',<')'>,2:12]
[@10,21:21='{',<'{'>,2:14]
[@11,27:27='x',<ID>,3:4]
[@12,29:29='=',<'='>,3:6]
[@13,31:31='x',<ID>,3:8]
[@14,33:33='+',<'+'>,3:10]
[@15,35:35='1',<INT>,3:12]
[@16,36:36=';',<';'>,3:13]
[@17,38:38='}',<'}'>,4:0]
[@18,40:39='<EOF>',<EOF>,5:0]
