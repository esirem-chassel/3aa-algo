# TP4 : Uno

# 0. Contexte

## 0.1 Description du jeu

Le Uno est un jeu qui se joue à 2 joueurs ou plus, avec un jeu de cartes spécial, comprenant 108 cartes réparties comme suit :
- 19 cartes rouges numérotées de 0 à 9 (en deux exemplaires sauf le 0, en un seul exemplaire)
- 19 cartes vertes numérotées de 0 à 9 (en deux exemplaires sauf le 0, en un seul exemplaire)
- 19 cartes jaunes numérotées de 0 à 9 (en deux exemplaires sauf le 0, en un seul exemplaire)
- 19 cartes bleues numérotées de 0 à 9 (en deux exemplaires sauf le 0, en un seul exemplaire)
- 8 cartes "+2" (2 de chaque couleur : rouge, vert, jaune, bleu)
- 8 cartes "inversion" (2 de chaque couleur : rouge, vert, jaune, bleu) présentant deux flèches entrelacées 
- 8 cartes "passer / passe ton tour" (2 de chaque couleur : rouge, vert, jaune, bleu) présentant un cercle rayé en bande, symbole d'interdiction en signalisation routière
- 4 cartes "Joker" (présentant un ovale écartelé multicolore sur fond noir)
- 4 cartes "+4" ou "Super Joker" (présentant une carte de chaque couleur, sur fond noir)

Au démarrage du jeu, on mélange le paquet, puis on distribue 7 cartes à chaque joueur. Puis la première carte est révélée.
Un joueur choisi démarre le premier tour, les tours se jouant par défaut dans le sens des aiguilles d'une montre.
A chaque tour, le joueur qui doit jouer place une carte (sur la précédente) ayant un point commun avec la carte actuelle :
- soit de la même couleur
- soit possédant le même symbole
- soit une carte "Joker" ou "+4"

S'il ne peut (ou ne désire) jouer aucune carte, alors le joueur doit piocher.
Il est à noter que si la pioche lui permet de jouer, il peut alors poser la carte en question.
Le tour passe au joueur suivant.

Certaines cartes ont des effets spéciaux :
- la carte "+2" force le joueur suivant à piocher deux cartes et à passer son tour, SAUF s'il possède une carte +2, qu'il peut alors poser. Le joueur suivant doit alors piocher 4 cartes, sauf s'il possède une carte +2, et ainsi de suite.
- la carte "passer" force le joueur suivant à passer son tour
- la carte "inversion" inverse le sens du jeu, ramenant le prochain joueur à jouer comme étant le précédent (note : à deux joueurs, cette carte a le même effet que "passer" )
- la carte "Joker" peut être posée quelque soit la couleur ou le symbole actuellement placé. Le joueur annonce alors une couleur : le joueur suivant considère alors que cette carte joker est de cette couleur
- la carte "+4" peut être posée quelque soit la couleur ou le symbole actuellement placé. Comme pour le Joker, le joueur l'ayant posé annonce une couleur, qui sera la couleur de la carte pour le tour suivant. Le joueur suivant doit alors annoncer s'il y a bluff ou non. "Bluff" signifie que le joueur qui a posé cette carte aurait pu poser une autre carte à la place. Un joueur appellé pour "bluff" révèle sa main; si le bluff est effectif, alors le joueur ayant posé le "+4" pioche 4 cartes à la place. Si le bluff est appellé mais qu'il n'est pas effectif, alors le joueur suivant doit piocher 6 cartes.

Une règle supplémentaire est le "Uno". Quand un joueur pose son avant-dernière carte, celui-ci doit dire "Uno" avant qu'un autre joueur annonce "Contre-Uno".

Il existe des règles supplémentaires, comme:
- les 0 et 7 qui permettent d'échanger des mains
- l'interception et la double pose
- cumul des +4
- pioche illimité

## 1.2 Adaptation

Afin de faciliter l'adaptation à moindre problèmes, nous allons adapter certains éléments.

On utilisera respectivement "+2", "+4", "JJ", "RV" et "PS" pour "+2", "+4", "Joker", "Inversion" et "Passer".
On affichera chaque carte en indiquant son type, suivi d'un espace et d'une lettre indiquant la couleur parmi "R", "J", "B", "V", "N".

A chaque tour, on affichera le plateau de jeu en ASCII.

Lors de l'affichage de la main du joueur, on indiquera un ordre des cartes, de 1 à N.

Lorsque l'utilisateur utilise un +4, on implémentera une probabilité aléatoire que l'ordinateur appelle au bluff.

Après la pose d'une carte du joueur "humain", on attendra une saisie utilisateur, pour passer au joueur suivant. Dans la majorité des cas, le joueur n'aura qu'à appuyer sur entrée.
S'il saisit "UNO" alors qu'il ne lui reste qu'une carte, tout va bien. S'il oublie de saisir "UNO" alors qu'il ne lui reste qu'une carte, alors il doit en piocher deux.
Enfin, s'il saisit "UNO" alors qu'il lui reste plus d'une carte, alors il doit en piocher deux.
On considérera que les joeuurs non-humains n'oublient jamais de crier "UNO" quand nécessaire.

## 1. Algorithmique

Décomposez les différents éléments de jeu en fonction, et préparez l'algorithme et/ou l'algorigramme de chaque foncion. Pensez à la fonction principale !

## 2. Développement

Lancez-vous dans le développement !
