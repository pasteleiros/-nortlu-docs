02 - Querys basicas

[[toc]]

---

# Strings

## Inserir dados 

```
SET "KEY" "VALUE"

ex:

SET "resultado:20-01-2020:megasena" "1,5,9,3,8,7"
SET "resultado:10-02-2020:megasena" "4,5,9,3,8,7"
SET "resultado:08-03-2020:megasena" "1,6,9,7,8,7"
SET "resultado:06-04-2020:megasena" "0,31,9,5,8,1"
SET "resultado:06-04-2020:quina"    "31,9,5,8,1"

```

---

## Recuperar valor

```
GET "KEY"

ex:

GET "resultado:20-01-2020:megasena"
GET "resultado:10-02-2020:megasena"
GET "resultado:08-03-2020:megasena"
GET "resultado:06-04-2020:megasena"
GET "resultado:06-04-2020:quina"   
```


---


## Deletar valor

```
DET "KEY"

ex:

DET "resultado:20-01-2020:megasena"
DET "resultado:10-02-2020:megasena"
DET "resultado:08-03-2020:megasena"
DET "resultado:06-04-2020:megasena"
DET "resultado:06-04-2020:quina"   
```


---

## Listar chaves

```
KEYS "<REGEX>"

ex:

---------------------------------------------
// O "KEYS *" (com asterisco) nos retorna todas as chaves armazenadas. Se quisermos filtrá-las pelo nome, basta fazer, por exemplo: 
<ip> KEYS *
1) "penultimo_sorteio"
2) "resultado:03-05-2015:megasena"
3) "resultado:17-05-2015:megasena"
4) "ultimo_sorteio"
5) "resultado:10-05-2015:megasena"
6) "antepenultimo_sorteio"
7) "resultado:15-04-2015:megasena"
8) "resultado:22-04-2015:megasena"

---------------------------------------------

<ip> KEYS "resultado:*-05-2015:megasena"
1) "resultado:03-05-2015:megasena"
2) "resultado:17-05-2015:megasena"
3) "resultado:10-05-2015:megasena"


---------------------------------------------
<ip> KEYS "resultado:1*-05-2015:megasena"
1) "resultado:17-05-2015:megasena"
2) "resultado:10-05-2015:megasena"


---------------------------------------------
// Se quisermos que a lacuna seja preenchida com apenas um caractere, utilizamos o "?" (ponto de interrogação):

<ip> KEYS "resultado:1?-05-2015:megasena"
1) "resultado:17-05-2015:megasena"
2) "resultado:10-05-2015:megasena"

---------------------------------------------
<ip> KEYS "resultado:?3-??-????:megasena"
1) "resultado:03-05-2015:megasena"


---------------------------------------------
<ip>KEYS "resultado:?7-??-????:megasena"
1) "resultado:17-05-2015:megasena"


---------------------------------------------

<ip> KEYS "resultado:?[37]-??-????:megasena"
1) "resultado:03-05-2015:megasena"
2) "resultado:17-05-2015:megasena"

```

---
---

# hash

## Inserir dados 

```
HSET "KEY" "CAMPO" "Values"

HMSET "KEY" "CAMPO1" "Values1" "CAMPO2" "Values2"

ex:

 HSET resultado:24-05-2015:megasena "numeros" "13, 17, 19, 25, 28, 32"
 HSET resultado:24-05-2015:megasena "ganhadores" 23

 HSET resultado:24-05-2015:megasena "numeros" "13, 17, 19, 25, 28, 32" "ganhadores" 23

```

---

## Recuperar valor

```
GET "KEY" "CAMPO"

ex:

<ip> HGET resultado:24-05-2015:megasena "numeros"
"13, 17, 19, 25, 28, 32"

<ip> HGET resultado:24-05-2015:megasena "ganhadores"
"23"  
```

---


## Deletar valor

```
HDET "KEY" "CAMPO"

ex:

HDET "resultado:20-01-2020:megasena"
HDET "resultado:10-02-2020:megasena"
HDET "resultado:08-03-2020:megasena"
HDET "resultado:06-04-2020:megasena"
HDET "resultado:06-04-2020:quina"   
```

---

# Comuns

## Definindo tempo de expiração

```
EXPIRE "KEY" <tempo em segundos>

ex

EXPIRE "resultado:06-04-2020:quina"  1800
```

---


## Ver tempo de expiração reestante

```
TTL "KEY" 

ex

TTL "resultado:06-04-2020:quina"
```

---

## Incrimentando valor de uma chave

```
INCR "KEY"
INCRBY "KEY" valor
INCRBYFLOAT "KEY" valor_float

---------------------------------------------
<ip> INCR pagina:/contato:25-05-2015
(integer) 10

<ip> INCR pagina:/contato:25-05-2015
(integer) 11

---------------------------------------------
<ip> INCRBY compras:25-05-2015:valor 15
(integer) 15

<ip> INCRBY compras:25-05-2015:valor 17
(integer) 32

---------------------------------------------

<ip> INCRBYFLOAT compras:25-05-2015:valor 10.50 
"42.5"
<ip> INCRBYFLOAT compras:25-05-2015:valor -0.50 
"42.0"
```

----
## Incrimentando valor de uma chave

```
DECR "KEY"
DECRBY "KEY" valor
DECRBYFLOAT "KEY" valor_float

---------------------------------------------
<ip> DECR pagina:/contato:25-05-2015
(integer) 10

<ip> DECR pagina:/contato:25-05-2015
(integer) 9

---------------------------------------------

<ip> DECRBY compras:25-05-2015:valor 2
(integer) 32

---------------------------------------------

<ip> DECRBYFLOAT compras:25-05-2015:valor 10.50 
"42.5"

```

----
----

# Bits

## Querys 

```
SETBIT "KEY"  "CAMPO" <0 ou 1> // insere
GETBIT "KEY"  "CAMPO"  // recupera
DELBIT "KEY"  "CAMPO"  // deleta
BITOP AND "NEW_KEY" "KEY1" "KEY2"  // conta os bits com duas chaves com o operador E
BITOP OR  "NEW_KEY" "KEY1" OR  "KEY2" //conta os bits com duas chaves com o operador OR
```
