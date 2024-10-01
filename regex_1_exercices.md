# Cours 1 - Exercices

Pour ce cours, les exercices se font sur le texte suivant, à copier dans [regex2](https://regex101.com/)



```
Testons le fonctionnement des regex.

Voici des dates (1600, 1634, 1700, 1709, 1800, 1825, 1861, 1900, 1975, 2000, 2023).

Voici une déclinaison: dominus domine dominum domini domino domino, domini domini dominos dominorum dominis dominis.
un underscore_ 

VOici que j'ai tapé deux majuscules de suite.. UNe     addition: 3+2=5. Une liste de formats: a0, a3, a4

Alors: "comment ça va?",     demanda-t-elle; "aaa! aa! ôô! eeehhhhh, aïe aïeaïe aïe aïeaïeaïe", repondit-il...
Clémence, Jean-Pierre, Louise, Anne-Marie,   Myriam, Colin, Marie-Christine   et Lou-Anne se promènent.
Ils évoquent l'anticonstitutionnalité, le déconstructivisme et    l'hyperprésidentialisation.
```


### Recherche de base


+ Rechercher plusieurs caractères qui se suivent dans le texte
+ rechercher `domine`, `domini`, `domino`
+ rechercher les points et les virgules
- chercher `il` et `elle` et les remplacer par `iel` (sur le site, choisir `tool -replace`)

### Classes de caractères

- chercher `dominos` et `dominis` (mais PAS `dominus`), par deux méthodes différentes
- rechercher toutes les dates

- chercher les dates à partir de 2000
- chercher les dates antérieures à 1800



### Classes de caractères prédéfinies


- Trouver la liste des formats papier (`a+chiffre`)
- Trouver les mots commençant par `a` qui ne sont pas des formats papier
- Trouver les caractères de ponctuation qui sont précédés d'un blanc, puis ceux qui sont suivis d'un blanc	


### Quantificateurs


- trouver toutes les occurrences où `aïe` est répété en un seul mot, et les remplacer par `ouille`
- Chercher toutes les occurrences de `dominus`
- Sélectionner les années
- Sélectionner les années antérieures à 1900
- Sélectionner les millésimes
- Trouver les mots qui, par faute de frappe, commencent par deux majuscules
- Sélectionner les prénoms composés
- Trouver les mots  de 15 lettres et plus, et les remplacer par `#@!+\`
- supprimer les espaces surnuméraires



**Pour s'entraîner chez soi**:
Faire les exercices 1 à 3 ici [regextutorial](http://regextutorials.com/excercise.html?Floating%20point%20numbers)
(les exercices suivants engagent des notions que nous n'avons pas encore vues)
