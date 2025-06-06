# TD1

## 1.0 - Reconnaissance

Donnez, pour chaque algorithme, le nombre de variables (arguments compris) et le nombre d'instructions.

### 1.1 - Algo 1

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

### 1.2 - Algo 2

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

### 1.3 - Algo 3

```
DEBUT algo3
  PARAM ENTIER x DEFAUT 1
  PARAM ENTIER y DEFAUT 0
  VARIABLE z ← APPEL algo1 AVEC a=x, b=y
  SORTIE APPEL algo2 AVEC x=(x - y), y=z
FIN
```

### 1.4 - Soit les appels suivants. Quel est le résultat de chaque appel ?

```
r1 ← APPEL algo1
r2 ← APPEL algo1 AVEC a=0, b=5
r3 ← APPEL algo1 AVEC a=-1, b=5
r4 ← APPEL algo2 AVEC a=3, b=3
r5 ← APPEL algo2 AVEC a=3, b=0
r6 ← APPEL algo2 AVEC a=0, b=3
r7 ← APPEL algo2 AVEC a=5, b=2
r8 ← APPEL algo2 AVEC a=0, b=1
r9 ← APPEL algo3
r10 ← APPEL algo3 AVEC a=1, b=2
r11 ← APPEL algo3 AVEC a=0, b=3
r12 ← APPEL algo3 AVEC a=0, b=5
```

### 1.5 - Soit l'algorigramme suivant :

```mermaid
flowchart TD
    A([askEven]) --> B[/Affiche "Saisir un entier ou 0 pour stopper"/]
    B --> C[/Saisie x/]
    C --> D{Est un nombre}
    D -->|?| B
    D -->|?| E{y égal à 0}
    E -->|Oui| Z([fin])
    E --> F[y ← x % 2]
    F --> G{y égal à 0}
    G -->|Oui| H[/Afficher "?"/]
    G -->|Non| I[/Afficher "?"/]
    H --> B
    I --> B
```

Remplacez les `?` et complétez les éventuels éléments manquants.

### 1.6 - Séparation
Séparez cet algorigramme en deux algorigrammes : `askEven` et `isEven`.
Le second algorigramme n'effectuera que la vérification pair/impair en retournant 1 si pair et 0 si impair. Aucun affichage ne sera fait.
Le premier algorigramme réalisera la demande à l'utilisateur et appellera `isEven`, puis affichera "pair" ou "impair" selon le résultat.


## 2.0 - Conception basique

### 2.1 - Echange naïf
Ecrire un algorigramme et un algorithme permettant d’échanger les valeurs de deux variables `xa` et `xb`. 

### 2.2 - Echange malin
Ecrire un algorithme permettant d’échanger les valeurs de deux variables numériques `xa` et `xb` sans utiliser d’autres variables. 

### 2.3 - Polynome basique
Ecrire un algorithme permettant de calculer la valeur de la fonction `f(x) = 3x² - 8x + 7` en fonction d'un paramètre `x`.

Tester l'algorithme avec les valeurs de `x` suivantes : `-2` , `10` , `5` et `3`

## 3.0 - Conception, on continue

### 3.1 - Facteur
Ecrire un algorigramme et un algorithme demandant à l'utilisateur un nombre `x` puis un nombre `y`, qui calcule `x<sup>y</sup>` et l'affiche. Vous ne pouvez utiliser de fonctions supplémentaires.

### 3.2 - Prix unitaire
Ecrire un algorigramme et un algorithme demandant à l’utilisateur un prix unitaire et un nombre d’articles. Cet algorithme devra pouvoir être exécuté avec un argument `taxrate` pour le taux de taxe. Informez l’utilisateur du prix TTC total et par article. Enfin, renvoyez le prix TTC total.

### 3.3 - H+1
Ecrire un algorithme qui, avec deux paramètres `h` et `m` (respectivement : heures et minutes), renvoi l’heure une minute après.

### 3.4 - Photocopies dégressives
Soit un magasin facturant une photocopie 20c l’unité avec un barème dégressif : au-delà de 10 photocopies, les vingt photocopies suivantes sont facturées 10c l’unité. Au-delà encore de ce nombre, chaque photocopie est facturée 8c.
Ecrire un algorigramme et un algorithme renvoyant, en fonction d’un nombre de photocopie, un prix total en euros (arrondi au cent).

