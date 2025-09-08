# TP3 : Makefile

# O. Contexte

L'objectif de ce TP est la rédaction et la compréhension globale d'un outil tel que make et son format Makefile dans le cadre d'un projet basique en C.

La maîtrise n'est pas attendue;
néanmoins les [outils de build](https://en.wikipedia.org/wiki/List_of_build_automation_software) sont largement utilisés, dans des langages tels que Java, C#, Javascript...

> [!Note]
> Même si Visual Studio nous "facilite" la fin en se débrouillant seul pour effectuer les builds,
> cela n'est valable que lorsqu'un projet est intégralement géré par Visual Studio,
> sans manipulation manuelle des fichiers.
> Cela vous confine à un seul système, à un seul IDE, à un seul contexte d'exécution (Windows, votre système),
> ce qui, de nos temps, n'est plus envisageable.

Pour ce projet, nous utiliserons Visual Studio Code, et non Visual Studio.

> [!Caution]
> L'usage de GCC sous Windows (ou d'autres outils de build) peuvent déclencher aisément des fausses alertes sur les antivirus classiques.
> Les moyens d'esquiver ceci sont incertains ou dangereux.
> Si cela vous arrive, il est conseillé d'effectuer une installation via WSL et d'utiliser C, GCC et make à travers WSL.
> Cela peut sembler effrayant, mais c'est en réalité plutôt simple.

# 1. GCC : la compilation manuelle

## 1.1 Avec un fichier

Pour commencer, créons un projet basique, que nous nommerons `mako`.
Créons un unique fichier `mako.c` :

```c
#include <stdio.h>

int main(void) {
    printf("Hello World");
    return 0;
}
```

Maintenant, compilons notre fichier. Nous allons le faire manuellement; c'est l'objectif aujourd'hui.

`gcc -c -Wall mako.c`

Cette commande lance GCC, en indiquant une compilation (`-c`), en activant les warning (`-Wall`) et en indiquant le ou les fichiers sources à compiler.
Listez les fichiers dans votre répertoire; notez ce qui est apparu.

A présent, nous allons effectuer le linking, afin de créer notre exécutable : `gcc -o Mako <nom du fichier généré>`.

> [!Note]
> En réalité, cette commande prend en second argument la liste des fichiers `.o` à link.

Notez le fichier qui est apparu; celui-ci est un exécutable ! Testez-le dans une console; "Hello World" devrait s'afficher.

Supprimez désormais les fichiers générés : `mako.o` et `Mako`.

## 1.2 Avec plus de fichiers

Nous allons créer un second fichier : `halo.c`. Celui-ci est simpliste :

```c
#include <stdio.h>

void halo() {
    printf("Hello World !\n");
}
```

Il s'agit de déporter notre fonction et sa dépendance "ailleurs".
Modifions donc notre fichier `mako.c` :

```c
#include "halo.c"

int main(void) {
    halo();
    return 0;
}
```

Lançons notre compilation, pour commencer : `gcc -c halo.c mako.c`. Constatez le nombre de fichiers générés.

Maintenant lançons notre linking... `gcc -o Mako halo.o mako.o`. Que se passe-t-il ?
Cette erreur peut être ignorée d'une certaine manière, mais nous allons d'abord tenter un coup de voodoo...

`gcc -o Mako mako.o`

Puis lancez l'exécutable généré. Nous reviendrons sur la raison de ce comportement; mais cela repose sur la différence entre définition et déclaration.

## 1.3 Avec des headers

L'erreur que vous avez vu est une erreur classique.
Dans notre cas précis, nous avons inclus de manière brouillonne le .c nécessaire dans le fichier source.
La définition et la déclaration sont alors au même endroit, et l'inclusion est réalisée lors du passage du préprocesseur, ce qui est son rôle (`#include` est une directive du préprocesseur, rappellez-vous !) car passe au tout début de la compilation.

Sauf que voilà : si votre fichier est nécessaire à plusieurs endroits, vous allez vous retrouver à inclure plusieurs fois le fichier, ce qui va introduire d'autres erreurs, contournables, mais à certains sacrifices. D'où l'usage de headers, entre autres.

Créons donc proprement notre `halo.h` :
```c
#include <stdio.h>

void halo();
```

Et modifions notre `halo.c` :

```c
#include "halo.h"

void halo() {
    printf("Hello World !\n");
};
```

Enfin, modifions notre `mako.c` :

```c
#include "halo.h"

int main(void) {
    halo();
    return 0;
}
```

Désormais, nous avons nos trois fichiers. Nous reste à les compiler : `gcc -c -Wall halo.c mako.c`.

Tentez, à tout hasard, d'effectuer un linking de `mako.o` : `gcc -o Mako mako.o` - que se passe-t-il ?

Eh oui, car `mako` fait désormais référence à quelque chose d'indéfini, car défini ailleurs : `halo()`.
Nous avons pu compiler, mais nous avons besoin de *lier* à la définition derrière.

Effectuons donc notre linking proprement : `gcc -o Mako halo.o mako.o`, et magie ! Nous obtenons notre exécutable, qui fonctionne parfaitement.

# 2. Make

Tout ceci était rigolo ou à défaut instructif.
Mais nous parlons ici d'un projet avec deux fichiers très minimalistes.
Rien que les TP que vous avez réalisé jusqu'ici contenait bien plus de codes et *normalement* plus de fichiers.

Imaginez devoir taper ces commandes A CHAQUE FOIS qu'un fichier est modifié, pour tester. L'enfer.

L'un des objectifs de make est de nous permettre de compiler aisément, en lui définissant des tâches, dépendant de fichiers (ou d'autres tâches) si et seulement si ces fichiers ont été mis à jour depuis.

Chaque relation ou règle de make se définit comme suit :
```make
produit : source
    commandes
```

> [!Tip]
> GNU Make repose intégralement sur... GNU.
> C'est un outil Unix/Linux basé sur POSIX, donc suivant un ensemble de règles.
> Si vous êtes familier de ces systèmes, gardez en tête que toutes ses règles s'y appliquent; vous pourrez commencer à vous douter de la puissance potentielle de l'outil.

## 2.1 La base du make

Testons donc en créant nos règles; créez un fichier `Makefile`:
```make
halo.o : halo.c
  gcc -c -Wall halo.c
mako.o : mako.c
  gcc -c -Wall mako.c
```

Ces règles permettent d'indiquer que si la dépendance `halo.c` a été modifiée depuis, on doit exécuter la commande `gcc -c -Wall halo.c` pour mettre à jour la cible `halo.o`. Et de même pour `mako.o` !

Ajoutons la règle pour notre programme, qui se base sur nos deux fichiers `halo.o` et `mako.o` :
```make
Mako : halo.o mako.o
  gcc -o Mako halo.o mako.o
```

L'astuce, néanmoins, est de définir des règles de priorité.
Pour éviter toute confusion, pour le moment, placez d'abord la règle concernant le programme avant la compilation des `.c` en `.o`; make recherche les règles en priorité en commençant par la première.

Testez votre fichier Makefile : lancez simplement `make` dans votre répertoire !

> [!Warning]
> Si vous obtenez une erreur concernant les séparateurs, il est probable que vous ayiez oublié le CM sur make, et que vous ayiez copié / collé le code indiqué.
> Dommage, il faut une tabulation, non des espaces, pour indenter les commandes. Vous êtes tombé dans mon piège.

## 2.2 Règles, cibles et dépendances

Une cible, en réalité, n'a pas besoin d'être un fichier réel.
Pareil pour une dépendance.

Dans notre cas, nous avons laissé des fichiers temporaires traîner dans notre répertoire : les fameux `.o`.
De même, une fois compilé et testé, notre exécutable n'est plus nécessaire.

Nous allons donc utiliser ce fait qu'une cible et une dépendance ne sont PAS nécessairement des fichiers pour créer une règle `clean` à la toute fin.

```make
clean :
  rm -f Mako *.o
```

Comme vous le constatez, la règle crée une cible `clean`, sans aucune dépendance. Comme cette cible n'est pas un fichier réel, elle s'exécutera toujours... si on lui demande !

Testez d'effectuer un `make`. Que se passe-t-il ?

Car dans notre Makefile actuel, aucune cible réellement exécutée ne dépend de `clean`. `make` n'a donc aucune raison d'exécuter cette règle... Sauf si on le lui demande explicitement, par exemple en effectuant `make clean`, que vous pouvez tester !

## 2.3 Variables UNIX

Tout à l'heure, j'ai divulgâché légèrement en parlant de POSIX.
Comme `make` se base sur ces stacks connues, on peut utiliser les syntaxes "classiques" de GNU/Linux, y compris dans la création de variables dans notre makefile.

Un exemple classique est la définition du... compilateur ! En effet, nous sommes sur GCC pour l'exercice, mais... d'autres compilateurs existent ! Mettons ça dans notre makefile.

```make
CC= gcc
Mako : halo.o mako.o
  $(CC) -o Mako halo.o mako.o
halo.o : halo.c
  $(CC) -c -Wall halo.c
mako.o : mako.c
  $(CC) -c -Wall mako.c
clean :
  rm -f Mako *.o
```

Comme dans la majorité des langages, une variable doit exister pour être utilisée.

Mais cela ne s'arrête pas à la simple définition de variables "simples" de types linéaires.
En GNU/Linux, on peut utiliser des listes de manière transparente.

```make
CC= gcc
OBJS= halo.o mako.o
Mako : $(OBJS)
  $(CC) -o Mako $(OBJS)
halo.o : halo.c
  $(CC) -c -Wall halo.c
mako.o : mako.c
  $(CC) -c -Wall mako.c
clean :
  rm -f Mako *.o
```

Ce fonctionnement nous sera TRES utile par la suite.

Il existe même des variables définies automatiquement, dont la valeur change selon le cas.
`$@` par exemple, contient le nom de la cible, ou `$^` qui contient le nom de toutes les dépendances.

Encore plus loin : on peut toujours utiliser les jokers POSIX, comme %, qui liste tous les éléments (fichiers) répondant au motif indiqué. `%.o` par exemple, va sélectionner chaque fichier `.o` !

Regardez cette règle :

```make
%.o: %.c
     $(CC) -o $@ -c $<
```

D'après-vous, que fait-elle ?

## 2.4 Encore plus loin !
