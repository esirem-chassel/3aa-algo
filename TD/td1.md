# TD1

## 1.0 - Reconnaissance

Donnez, pour chaque algorithme, le nombre de variables (arguments compris) et le nombre d'instructions.

### Algo 1

```
DEBUT algo1
  PARAM ENTIER a DEFAUT 1
  PARAM ENTIER b DEFAUT 0
  VARIABLE r ← 0
  a ← a + 1
  b ← b × a
  r ← b - a
  SORTIE r
FIN
```

### Algo 2

```
DEBUT algo2
  PARAM ENTIER x DEFAUT 1
  PARAM ENTIER y DEFAUT 1
  VARIABLE ENTIER a ← 1
  VARIABLE ENTIER b ← 1
  VARIABLE ENTIER c ← 1
  a ← a × x + y
  b ← b × y + x
  r ← c × (x + y)
  SORTIE (a × b) - c
FIN
```

### Algo 3

```
DEBUT algo3
  PARAM ENTIER x DEFAUT 1
  PARAM ENTIER y DEFAUT 0
  VARIABLE z ← APPEL algo1 AVEC a=x, b=y
  SORTIE APPEL algo2 AVEC x=(x - y), y=z
FIN
```
