# TP5 : Faster!

## 0. Contexte

### 0.1 Objectif

L'objectif de ce TP est de s'entraîner à certaines notions plus avancées en C, comme l'usage de static ou encore de librairies externes.
Nous allons réaliser un petit jeu de frappe rapide : une phrase est donnée, le joueur doit saisir la phrase le plus vite possible.
En fonction de la précision de la frappe (fautes de frappes) et du temps passé, un score est calculé.

### 0.2 Appels prédéfinis

Certaines fonctions sont à utiliser.

#### Calcul du temps

Sous Windows, `GetSystemTime` est à utiliser. Cette fonction est contenue dans `Windows.h`, une librairie standard sous Windows. Elle utilise un `SYSTEMTIME` sous la forme d'un pointer.
Sous Linux, `gettimeofday` est à utiliser. Cette fonction est contenue dans `sys/time.h`, une librairie standard sous Linux. Elle renvoie un `time_t` sous la forme d'un pointer.

## 1. Algorithmique et contraintes

### 1.1 Algorithme/Algorigramme

Vous devez préparer un algo (gramme ou rithme) de votre programme, en prenant en considération :
- qu'on puisse "piocher" des phrases aléatoires (possiblement depuis une liste prédéfinie dans un fichier)
- le jeu se poursuit sur N itérations, avec le score se cumulant à chaque itération, jusqu'à ce que le joueur arrête (en laissant sa saisie vide par exemple)
- on puisse enregistrer son score comme "record" dans un fichier dédié

### 1.2 Calcul de la distance

Vous devez implémenter une fonction `levenshtein` qui calculera la distance levenshtein entre deux chaînes, avec un ratio de `add=1;del=1;replace=1`.
Cela signifie que toute opération d'ajout, suppression ou remplacement aura un poids de "1". La distance entre `tata` et `fadas` est de 3, par exemple (deux remplacements, 1 ajout).

### 1.3 Calcul de la précision

Vous devez implémenter une focntion de calcul de la précision, en pourcentage.
En fonction de la distance, cette fonction doit retourner un pourcentage de précision entre une chaîne de référence, et une chaîne donnée, 100% étant une chaîne identique.

### 1.4 Calcul du score

La calcul du score sera réalisé via la formule : `(100 * len * accuracy) / timeDiff` avec
- `len` la longueur de la chaîne en caractères
- `accuracy` la précision en pourcentage
- `timeDiff` la différence de temps en millisecondes

### 1.5 Différence temporelle

Via l'usage des différentes fonctions de relevé temporel, vous devez implémenter deux fonctions :
`startChrono` qui va "démarrer" un chronomètre et `stopChrono` qui va le stopper et renvoyer la différence, en millisecondes, de temps passé.

## 2.0 A vous !

A vous d'implémenter le jeu !
