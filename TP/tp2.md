# TP2

## 0. Contexte

L'objectif est ici d'implémenter une partie des algorithmes préparés lors du TD2, en C.

## 1. Menu

Implémentez les fonctions de base.

### 1.1 EGAL

Créez la fonction `EGAL` qui prend deux paramètres :
- `gauche`, une chaîne
- `droite`, une chaîne

Cette fonction vérifie si les deux chaînes sont égales en ignorant la casse.

Il est à noter que les librairies de comparaison de chaînes changent selon votre système :

| Système | Librairie | Comparaison sensible à la casse | Comparaison insensible à la casse |
| --- | --- | --- | --- |
| Windows | string.h | strcmp | _stricmp |
| Linux | strings.h | strcmp | strcasecmp |

Plutôt que d'utiliser des booléens artificiellement, renvoyez 1 si les chaînes sont égales, 0 sinon.

### 1.2 DANSLISTE

Créez la fonction `DANSLISTE` qui prend trois paramètres (dont un facultatif) :
- `val`, le caractère à vérifier
- `liste`, la liste de caractères, sous la forme d'une chaîne de caractères
- `ignorerCasse`, un entier pour ignorer la casse (`1`) ou non (`0`)

Cette fonction vérifie si la valeur `val` est dans la liste `liste` et renvoie un entier (1 si égal).

### 1.3 POGNON

Créez la fonction `POGNON` qui prend un paramètre entier `tour` et renvoie l'argent espéré pour le tour,
selon la formule mathématique :
```math
a(n) = a(n−1) ⋅ 2.16
```

Avec n étant le numéro du tour, sachant que $$a(1)=1000$$.

## 2. Jeu principal

Afin d'implémenter votre code, certaines fonctions sont fournies (note : ces fonctions divergent légèrement de celles du TD2 !).

- `LSQUESTIONS` qui donne la liste des questions disponibles, sous forme de clefs (entiers)
- `UNEQUESTION` qui, à partir d'une clef (entier) de question, renvoie une liste de 4 questions sous la forme : `[Contenu, Réponse A, Réponse B, Réponse C, Réponse D, Réponse valide]`
- `AJOUTTAB` qui, à partir d'un pointeur vers le premier élément de tableau d'entiers, la taille précédente du tableau et une valeur entière, renvoie le tableau modifié avec la valeur ajoutée

L'implémentation de ces fonctions est disponible en annexe.

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

## Annexes

### Liste de questions (initialisation globale)

```c
char* ALLQUESTIONS[20][6] = {
  {"Quelle est la capitale de l'Italie ?", "Madrid", "Rome", "Athènes", "Lisbonne", "B"},
  {"Qui a peint la Joconde ?", "Léonard de Vinci", "Michel-Ange", "Raphaël", "Donatello", "A"},
  {"Quel est le symbole chimique de l'or ?", "Ag", "Au", "Fe", "Pt", "B"},
  {"En quelle année a eu lieu la chute du mur de Berlin ?", "1987", "1989", "1991", "1993", "B"},
  {"Qui a écrit 'Les Misérables' ?", "Victor Hugo", "Émile Zola", "Molière", "Balzac", "A"},
  {"Quel est le plus grand océan du monde ?", "Atlantique", "Pacifique", "Arctique", "Indien", "B"},
  {"Combien y a-t-il de planètes dans le système solaire ?", "7", "8", "9", "10", "B"},
  {"Quelle est la monnaie officielle du Japon ?", "Yuan", "Yen", "Won", "Ringgit", "B"},
  {"Qui a découvert la pénicilline ?", "Louis Pasteur", "Alexander Fleming", "Marie Curie", "Joseph Lister", "B"},
  {"Quel est le plus long fleuve du monde ?", "Nil", "Amazon", "Yangtsé", "Mississippi", "B"},
  {"Quelle est la langue la plus parlée dans le monde ?", "Anglais", "Espagnol", "Mandarin", "Hindi", "C"},
  {"Qui est l'auteur de '1984' ?", "George Orwell", "Aldous Huxley", "Jules Verne", "Isaac Asimov", "A"},
  {"Quel pays a gagné la Coupe du monde de football 2018 ?", "Brésil", "France", "Allemagne", "Argentine", "B"},
  {"Quelle planète est surnommée la planète rouge ?", "Vénus", "Mars", "Jupiter", "Mercure", "B"},
  {"Quel est le nombre de côtés d'un hexagone ?", "5", "6", "7", "8", "B"},
  {"Qui a formulé la théorie de la relativité ?", "Newton", "Einstein", "Galilée", "Copernic", "B"},
  {"Quel est le plus grand désert du monde ?", "Sahara", "Gobi", "Kalahari", "Antarctique", "D"},
  {"Quel métal est liquide à température ambiante ?", "Fer", "Mercure", "Plomb", "Aluminium", "B"},
  {"Quelle est la capitale du Canada ?", "Toronto", "Montréal", "Ottawa", "Vancouver", "C"},
  {"Combien de cordes a un violon ?", "4", "5", "6", "7", "A"}
};
```

### Ajout d'un élément dans un tableau

```c
int* AJOUTTAB(int* tab, int actualSize, int x) {
	int* r = realloc(tab, (1+actualSize) * sizeof(int));
	r[actualSize] = x;
	return r;
}
```

### Liste complètes des clefs de questions

```c
int* LSQUESTIONS() {
	int* r = malloc(20 * sizeof(int));
	for (int i = 0; i < 20; i++) { r[i] = r; }
	return r;
}
```

### Obtention d'une question par sa clef

```c
char** UNEQUESTION(int k) {
	return ALLQUESTIONS[k];
}
```
