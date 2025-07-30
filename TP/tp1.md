# TP1 : Implémentation

## Contexte

L'objectif est d'implémenter les différents algorithmes préparés durant le TD1.

## Outils / Démarrage

Ce TP est guidé, et se base sur une installation de Visual Studio (Community Edition).

Lancez Visual Studio, puis sélectionnez "Créer un nouveau Projet".
Dans la liste des templates de projets proposés, sélectionnez "Application Console".
Laissez les paramètres suivants par défaut (vous pouvez bien sûr personnaliser le nom du projet et son emplacement).

> [!Note]
> Par défaut, cela crée un projet C++.
> Il n'existe pas de distinction entre C et C++ dans Visual Studio.
> Seule l'extension du fichier (`.c` au lieu de `.cpp`) fait une différence.

### Hello World

Dépliez l'encadré des fichiers sources, puis faites un clic droit, Ajouter, Nouvel élément.

> [!Tip]
> Visual Studio fonctionne sur un mode d'ajout au projet.
> Un fichier existant n'est pas suffisant pour qu'il soit ajouté à un projet,
> il faut l'ajouter manuellement.
> N'effectuez pas d'opération d'ajout / modification / suppression de fichiers hors de Visual Studio,
> ou vous devrez effectuer des opérations supplémentaires pour synchroniser vos modifications avec le projet VS.

Nommez votre fichier "basics.c" et validez.
Supprimez le fichier CPP initialement créé par Visual Studio et portant le même nom que votre projet.

Dans le fichier `basics.c`, ajoutez le code minimal suivant, afin de tester si tout se passe bien :

```c
#include <stdio.h>

int main() {
	printf("Hello World !");
	return 0;
}
```

Une fois le fichier sauvegardé, testez votre code.

Une console devrait s'ouvrir, affichant "Hello World !".

`main` est une fonction. Pour rappel, une fonction est un ensemble de code pouvant prendre des paramètres, pouvant renvoyer une valeur, et réalisant une tâche précise.
Les fonctions sont les principaux découpages de votre code. Pour qu'une fonction puisse être appellée (utilisée), elle doit être définie et connue du code qui l'appelle.

En C, la fonction `main` est particulière.
Une fonction `int main(void)` ou `int main(int charc, char* argv[])` est le point d'entrée, la fonction qui sera exécutée au lancement du programme.
Nous rentrerons dans le détail plus tard, mais cela signifie que votre projet ne devrait contenir idéalement qu'une seule fonction `main`.

## Programme

Conservez votre `main`, mais retirez le `printf`.
Nous allons utiliser le main pour tester différentes fonctions qui implémenterons les algorithmes du TD1.

### algo1

Implémentons `algo1`.
Cet algorithme prend deux paramètres, `a` et `b`, et renvoie un calcul par rapport aux paramètres donnés.

> [!Warning]
> C ne supporte pas, par défaut, les arguments optionnels.
> Les manières d'implémenter des arguments optionnels sont pénibles et/ou contre-intuitifs.

Dans votre fichier `basics.c`, ajoutez, n'importe où dans votre programme mais à l'extérieur du `main` et après l'`include`, une fonction `int algo1(int a, int b)`.

<details>
  <summary>Proposition de solution</summary>

```c
int algo1(int a, int b) {
	int r = 0;
	a = a + 1;
	b = b * a;
	r = b - a;
	return r;
}
```
  
</details>

Puis testez des appels :
```c
int x1 = algo1(1, 0);
printf("%d\n", x1);
int x2 = algo1(10, 5);
printf("%d\n", x2);
```

> [!Note]
> `printf()` est une fonction qui réalise de l'affichage en suivant un formatage.
> Le premier paramètre est le formatage.
> Il utilise des [caractères spéciaux commençant par `%` afin d'inclure des paramètres dans l'affichage](https://cplusplus.com/reference/cstdio/printf/).
> `%d`, par exemple, indique un "décimal entier signé".
> Ensuite, chaque autre paramètre de `printf` est utilisé dans le même ordre.
> Ainsi, ce premier `%d` sera remplacé par une représentation entière de `x1`.
> Enfin, `\n` est le caractère standard de retour à la ligne.

Réécrivez le code exemple pour qu'il n'y ai qu'un seul printf des deux variables `x1` et `x2`.

### algo2 et algo3

Sur le même principe, implémentez `algo2`, ainsi que `algo3`.
N'oubliez pas de tester vos codes en utilisant la fonction `main` !

### Test 1.4

Remplacez le code de votre main par une implémentation du code de la partie 1.4 du TD1.

## Nouvel algo

Nous allons implémenter la méthode `askEven`, mais nous allons le faire un peu plus proprement.

### askEven

Jusqu'ici, nous avons tout placé dans un unique fichier où se situait notre `main`.
Dans la pratique, les projets de programmation contiennent en grand nombre de lignes,
et tout placer dans un même fichier alors que tout n'est pas forcément utilisé au même moment serait,
en plus d'être un cauchemar pour tout développeur, pas forcément performant.

Créez un nouveau fichier `askeven.c` dans lequel nous allons placer notre définition de fonction `void askEven()`.
Ensuitez, appellez, dans votre main, askEven :

```c
#include <stdio.h>

int main() {
	askEven();
	return 0;
}
```

Testez votre code. Que se passe-t-il ?

Ce problème vient du fait que `askEven` n'est pas connue.

Par exemple, la fonction `print()` n'est utilisable que parce que nous avons réalisé un `#include <stdio.h>` dans notre `basics.c`.

Incluons notre fichier `askeven.c` dans `basics.c` : `#include "askeven.c"` et testez à nouveau. Que se passe-t-il ?

> [!Caution]
> Lorsque vous décomposez votre code en fichiers,
> vous devez être rigoureux.
> Un fichier `.h` va contenir la déclaration d'une ou plusieurs fonctions.
> Un fichier `.c` va contenir la définition de ces fonctions, et va inclure le `.h` correspondant ainsi que tous les `.h` nécessaires.
> Ainsi, nous n'incluons que les `.h` lorsque nous avons besoin de fonctions, ce qui est plus léger et logique.
> Attention à ne pas metre de définition de fonctions dans les `.h`.
> Cela fonctionne, certes, mais cela défait tous les principes de séparation de rôles !
> Enfin, la différence entre `#include <...>` et `#include "..."` provient du fait que dans le premier cas, nous incluons des librairies externes au code du projet.

Créons donc un fichier `askeven.h` contenant la déclaration de la fonction. Incluons ce `.h` dans chacun des deux fichiers `.c`.

Pour éviter des inclusions récursives, ajoutons un `#pragma once` au début de notre `.h`, si ce n'est déjà fait.

Testons à nouveau notre code !

<details>
  <summary>Proposition de solution (sans contenu)</summary>
  
**basics.c**
```c
#include <stdio.h>
#include "askeven.h"

int main() {
	askEven();
	return 0;
}
```

**askeven.h**
```c
#pragma once
void askEven();
```

**askeven.c**
```c
#include <stdio.h>
#include "askeven.h"

void askEven() {
	printf("maybe");
}
```

</details>

### isEven

Sur le même principe de séparation, créez la fonction `isEven`, en suivant les mêmes concepts (vous aurez donc un `iseven.h` et un `iseven.c`...).

## Implémentations partie 2

En suivant tous les principes vus jusqu'ici, implémentez et testez les algorithmes de la partie 2.

## Implémentations partie 3

En suivant tous les principes vus jusqu'ici, implémentez et testez les algorithmes de la partie 3.

Attention, vous pourriez avoir besoin de réaliser plusieurs fonctions pour chaque algorithme !
