# trab-perso2-2022b-AlejandroBrites
trab-perso2-2022b-AlejandroBrites created by GitHub Classroom

# RECURSÃO EM PROLOG

  A recursão ocorre na programação quando uma função chama a si mesma. Normalmente esse tipo de recurso é usado para resolver problemas grandes, dividindo os mesmos em problemas menores de mais fácil resolução, facilitando assim a resolução final do problema.

Existem muitas linguagens de programação que utilizam recursão e Prolog também é uma delas. Vejamos alguns exemplos de aplicações de recursão em Prolog e como eles são feitos.

```Prolog
genitor(Elizabeth,Charles).
genitor(Charles,William).
genitor(William,George).

descendentev1(X,Y) :- genitor(Y,X).                               %1
descendentev1(X,Y) :- genitor(Y,Z), genitor(Z,X).                 %2
descendentev1(X,Y) :- genitor(Y,W), genitor(W,Z), genitor(Z,X).   %3
```

O código prolog acima detecta descendência direta, de até 3 gerações de diferença, em uma árvore genealógica.

A linha %1 detecta o parentesco de 1 geração de distância.
A linha %2 detecta o parentesco de 2 gerações de distância.
A linha %3 detecta o parentesco de 3 gerações de distância.

Porém para cada geração que a árvore aumente será necessário modificar o código, pois ele tem uma linha de código para cada geração. Para resolver esse problema iremos utilizar a recursão para fazer o código não depender de um número de gerações fixo.

```Prolog
genitor(Elizabeth,Charles).
genitor(Charles,William).
genitor(William,George).

descendentev2(X,Y) :- genitor(Y,X).
descendentev2(X,Y) :- genitor(Y,Z),descendente(X,Z).                %4
```

Com o uso de recursão o código acima irá resolver o problema de detecção de descendência independente do número de gerações pois o linha de código (%4) irá chamar a função “descendentev2” recursivamente 1 vez para cada geração, desse modo detectando qualquer descendência direta.


Outro problema clássico que pode ser resolvido por recursão é o cálculo do fatorial.

5! = 5*4*3*2*1
5! = 120

```Prolog
fatorial(0,1).
fatorial(N,F) :- N > 0,
                 N1 is N-1,
                 fatorial(N1,F1),
                 F is N * F1.
```

O código em Prolog acima irá calcular o fatorial de qualquer número, pois a função “fatorial(N,F)” sempre irá chamar ela mesma de maneira recursiva passando um parâmetro cada vez menor até chegar no valor zero onde será resolvida pela função “fatorial(0,1)”. Quanto maior for o número do qual o fatorial for calculado, maior será o número de chamadas recursivas que o programa irá executar.

# LISTAS EM PROLOG

Em Prolog as listas são representadas por seus elementos contidos entre “[]”.

Exemplos:

* [1, 2, 3, 4, 5, 6]
* [A, B, C]
* [3.1, 4.5, 7.3]

## Recurso Pipe ( | )

Em Prolog existe um recurso em lista chamado Pipe ele é representado pelo símbolo “ | ”. Sua função é separar a lista em duas partes sendo a primeira a sua Cabeça (Head) e a sua Cauda (Tail).

Cabeça (Head): Corresponde ao primeiro elemento da lista.
Cauda (Tail): corresponde aos demais elementos da lista com exceção da Cabeça.

Vamos começar com uma aplicação simples.

```Prolog
finalv1(X,[X]).
```

O código acima irá responder se um determinado elemento é o último elemento de uma determinada lista, porém só irá funcionar para listas com um único elemento.

É possível usar recursão para melhorar esse funcionamento.

```Prolog
finalv2(X,[X]).
finalv2(X,[ _ | T ]) :- finalv2(X,T).
```

Já esse outro código detecta se um determinado elemento é o último elemento de uma determinada lista, e ele funciona para lista de qualquer tamanho. Isso se deve ao fato de ele chamar recursivamente o predicado “finalv2” passando como parâmetro o próprio elemento de comparação “X” e a “Tail” da lista, todos os elementos da lista exceto o primeiro. Desse modo a cada chamada será enviado uma lista com um elemento, até ser enviada uma lista vazia.

Vamos ver outro exemplo de aplicação com listas.

```Prolog
pertencev1(X, [ X | _ ]).                             %1
pertencev1(X, [ _ | [ X | _ ] ]).                     %2
pertencev1(X, [ _ | [ _ | [ X | _ ] ] ]).             %3
pertencev1(X, [ _ | [ _ | [ _ | [ X | _ ] ] ] ]).     %4
```

O código acima detecta se um elemento X pertence a uma lista Y (de no máximo 3 elementos).

A linha %1 detecta se o elemento está na primeira posição.
A linha %2 detecta se o elemento está na segunda posição.
A linha %3 detecta se o elemento está na terceira posição.

Assim como no exemplo da árvore genealógica, para cada unidade de tamanho que a lista aumente será necessário adicionar uma linha nesse detector.

```Prolog
pertencev2(X,[X|_]).
pertencev2(X,[_|T]) :- pertence(X,T).
```

Por outro lado, esse código detecta se um elemento X pertence a uma lista Y, de qualquer tamanho.
Isso se deve ao fato deste código chamar recursivamente a função “pertencev2”, enviando como parâmetro a Cauda(Tail) da lista que está sendo analisada de maneira recursiva.

Em outras palavras, o código irá verificar se o elemento não se encontra na primeira posição, caso não se encontre irá chamar a função pertence usando como parâmetro a Cauda da lista original, ou seja, irá eliminar apenas o primeiro elemento que já foi verificado anteriormente.

Com isso, foi mostrado o uso básico de recursão em Prolog, os conceitos básicos de Lista em Prolog e o uso de recursão com Listas. Existem diversas outras aplicações para a recursão.

# Link do repositório no Replit

https://replit.com/@AlejandroBrites/Trabalho-Individual-02-Paradigmas#main.pl

Para executar o programa digite no terminal "swipl main.pl" para abrir o programa "main.pl".
