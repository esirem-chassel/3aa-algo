# TD2

## 0. Contexte

### 0.1 Objectifs

L'objectif de cet exercice est d'écrire un algorithme de "menu" en console avec vérification de saisie.
Le support sera un jeu de "questions".
Le joueur a 10 tours de jeu. A chaque tour, une question est posée, et 4 réponses possibles sont données.
Si la réponse est valide, le joueur remporte le tour, et la cagnotte est augmentée.
Si la réponse n'est pas valide, le joueur perd l'ensemble de la cagnotte.
A chaque tour, le joueur peut décider de tenter la question ou d'abandonner et ainsi encaisser la cagnotte.

### 0.2 Consignes

Sont demandés, pour le programme principal et chaque fonction :
- l'algorithme, en langage "naturel"
- un algorigramme

### 0.3 Fonctions prédéfinies

Les fonctions suivantes sont fournies :
- `VERIF` qui prend deux paramètres : une valeur et un type sous la forme d'un entier
  - 0 : chaîne
  - 1 : entier
  - 2 : flottant
- `LSQUESTIONS` qui donne la liste des questions disponibles, sous forme de clefs
- `UNEQUESTION` qui, à partir d'une clef de question, renvoie une liste sous la forme : `[Contenu, Réponse A, Réponse B, Réponse C, Réponse D, Réponse valide]`
- `MAJ` qui transforme une chaîne en majuscules
- `MIN` qui transforme une chaîne en minuscules
- `MST` qui renvoie le timestamp UNIX actuel
- `LIRENB` qui effectue une lecture **non-bloquante** d'une saisie utilisateur. Cette fonction prend un paramètre : le nom d'une fonction à exécuter une fois qu'une saisie utilisateur est détectée et validée

## 1.0 Fonctions de base

### 1.1 EGAL

Créez la fonction `EGAL` qui prend deux paramètres :
- `gauche`, une chaîne
- `droite`, une chaîne

Cette fonction vérifie si les deux chaînes sont égales en ignorant la casse.

### 1.2 DANSLISTE

Créez la fonction `DANSLISTE` qui prend trois paramètres (dont un facultatif) :
- `val`, la valeur à vérifier
- `liste`, la liste
- `ignorerCasse`, un booléen pour ignorer la casse (`VRAI`) ou non (`FAUX`) - par défaut `FAUX`

Cette fonction vérifie si la valeur `val` est dans la liste `liste` et renvoie un booléen.

### 1.3 POGNON

Créez la fonction `POGNON` qui prend un paramètre entier `tour` et renvoie l'argent espéré pour le tour,
selon la formule mathématique :
```math
a(n) = a(n−1) ⋅ 2.16
```

Avec n étant le numéro du tour, sachant que $$a(1)=1000$$.

## 2.0 Jeu de base

### 2.1 Menu

Créez le menu initial, afin de demander à l'utilisateur s'il souhaite :
- `[J]ouer`
- `[Q]uitter`

Si l'utilisateur choisit "Q" (peu importe la casse), le programme s'arrête.
Si l'utilisateur choisit "J", le jeu se lance au premier tour.
Si la saisie ne correspond à rien, demandez à nouveau à l'utilisateur.

### 2.2 TOUR

Créez la fonction `TOUR`, qui prend un paramètre entier, le numéro du tour, ainsi que la liste des questions déjà posées (sous forme de clefs).
Dans cette fonction, obtenez une question qui n'a pas déjà été posée.
Puis, affichez la question, suivie des réponses, et attendez la saisie de l'utilisateur.
Une fois la saisie effectuée, si celle-ci correspond à une des réponses (A, B, C ou D), affichez le résultat.
Si le joueur a perdu, revenez au menu principal.
Si la joueur a gagné, affichez la cagnotte, puis (si le tour est inférieur à 10) demandez si le joueur souhaite `[c]ontinuer` ou `[a]rrêter`.
Si le joueur arrête, il remporte la cagnotte et le programme s'arrête.
Si le joueur continue, passez au tour suivant.
Si le joueur gagne au dernier tour, le programme s'arrête.

## 3.0 Extenstion

### 3.1 Timer

Implémentez le timer.
Pour cela, utilisez la fonction `LIRENB` pour effectuer une lecture non-bloquante, encapsulée dans une boucle `TANTQUE` vérifiant un écart de temps.
Si cet écart de temps est supérieur à 30, et qu'aucune saisie n'a été réalisée, la réponse est considérée comme fausse.

## Annexes

### Format de fichier

> [!Note]
> Cet encart est donné à titre informatif

Chaque question est dans un format dédié, dans un fichier `.qpdp`.
Le nom du fichier est utilisé en tant que clef (le fichier `abc.qpdp` a donc pour clef `abc`).
```
===
Contenu de la question
=A=
Réponse A
=B=
Réponse B
=C=
Réponse C
=D=
Réponse D
=X=
```

X est remplacé par A, B, C ou D selon la bonne réponse.
