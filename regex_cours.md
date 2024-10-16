# Les Regex

## Introduction

- Regex: *regular expressions*, expressions régulières (ou expressions rationnelles)
- Une regex est une chaine de caractères, un motif (*pattern*) qui a pour rôle de décrire un ensemble de caractères possibles.
- Les regex sont donc   *la description formelle d'un ensemble de possibilités, selon une syntaxe donnée*, et non un langage.C'est cette syntaxe que l'on va apprendre.
- Elles sont interprétées par des moteurs, soit *via* une interface graphique (par le biais d'un Clt F par exemple) soit sans interface graphique (dans un script, dans un terminal). 
- On peut les utiliser par exemple: avec Python, Perl, Java,... dans certaines commandes UNIX (`grep`,...), dans des traitements de texte (LibreOffice) et des éditeurs de texte (Texstudio, Vim).
	
- Le moteur teste chaque caractère d'une chaîne de caractères. Si un caractère testé correspond au premier caractère de la regex, le moteur teste alors le caractère suivant, etc. Si un ensemble de caractères correspond à l'ensemble de la regex, il est considéré comme une occurrence, et le moteur passe à la suite du texte à traiter.

**nb** Il y a parfois selon les langages des spécificités concernant l'utilisation des Regex; certaines seront mentionnées dans ce cours.

### Ressources

- Un site pour construire et tester ses Regex: [regex2](https://regex101.com/)
- Un site d'exercices pour s'entraîner aux Regex; [regex_tutorial](http://regextutorials.com/index.html)

## Syntaxe

### Recherche simple/concaténation/alternative

 - `a`: on cherche le caractère "a"
- `.`: on cherche n'importe quel caractère.
- Plusieurs caractères à la suite sont concaténés: on les cherche ensemble. Ex `ab`, `a.`
- `|`: = OU. `moi|toi` = on cherche "moi" ou "toi"


*opérateurs:* caractères spéciaux, qui ont une sémantique particulière, par opposition aux  *caractères littéraux*, qui ne représentent qu'eux-mêmes. Les opérateurs sont: 
 `( ) [ ] . * ? + ^ | $  - \`

*échapper un caractère*: pour chercher un des des opérateurs, il faut l'*échapper* en le faisant précéder du caractère `\`. Par exemple, pour chercher un point, il faut taper `\.`




### Classes de caractères

 *classe de caractères*: une classe de caractères, entre crochets, définit un *ensemble de caractères* qui pourront correspondre (*match*) à la recherche d'un caractère.

- `[abc]`: recherche a, b ou c
- `[a-z] [A-Z] [0-9]`: recherche un caractère dans l'intervalle donné. `[a-zA-Z]` recherche ainsi n'importe quelle lettre en minuscule ou majuscule; `[a-zA-Z0-9]` cherche aussi les nombres
-  `[^aei]`: recherche n'importe quel caractère à l'exclusion de ceux indiqués après le `^` 

**nb**: Selon les moteurs, les caractères Unicode sont pris en compte (dans LibreOffice par exemple), ou Unicode doit être explicitement indiqué; cela signifie que le caractère `é`, par exemple, n'est pas forcément reconnu par l'intervalle `[a-z]`.

- Pour éviter d'avoir à taper les classes les plus fréquentes, il existe des classes prédéfinies.

### Rechercher des caractères unicodes

-  Pour rechercher un caractère unicode par son encodage, il faut taper `\x{code du caractère}`. Exemple: le s long (ſ) est encodé U+017F. Pour le rechercher, il faut taper `\x{O17F}`
- Il est possible de créer des classes avec les encodages unicode. Par exemple, l'alphabet syriaque est encodé dans le bloc  U+0700 à U+074F (source: [wikipedia](https://fr.wikipedia.org/wiki/Alphabet_syriaque). Pour rechercher n'importe quel caractère en syriaque, il faut donc taper `[\x{0700}-\x{074F}]`

- **Nb**: selon les langages de programmation, ne pas oublier de mettre le "flag" indiquant que le cherche en unicode. 

- En python, la syntaxe est `\u+code du caractère`. Exemple: `\u017F` pour le s long. Pour plus de précisisons, voir par exemple ici : [real python](https://realpython.com/python-encodings-guide/)


### Classes de caractères prédéfinies (classes d'équivalence)

|Classes POSIX|Raccourcis|Equivalent|
|-- |-- |-- |
|`[:word:]`|`\w`|	`[a-zA-Z0-9_]` (caractère alphanumérique et `_`)|
||`\W`|	`[^a-zA-Z0-9_]` (inverse de `\w`) |
|`[:alpha:]`||`[a-zA-Z]` (lettre)|
|`[:lower:]`||`[a-z]` (lettre en minuscule)|
|`[:upper:]`||`[A-Z]` (lettre en capitale)|
|`[:digit:]`|`\d`|	`[0-9]` (caractère numérique)|
||`\D`|	`[^0-9]` (caractère non numérique)|
|`[:space:]`|`\s`| `[ \t\n\x0B\f\r]` (n'importe quel caractère d'espacement: espace, retour de chariot, tabulation..)|
||`\S`|`[^\s]` (n'importe quel caractère qui n'est pas un espacement)|
|`[:punct:]`||caractère de ponctuation|
|`[:blank:]`|`\h`|n'importe quel caractère blanc (mais pas les retours à la ligne)|

- Le standard POSIX a été à l'origine rédigé pour UNIX. POSIX est un standard qui définit 12 classes. 
- Les classes POSIX non abrégées (entre crochets) doivent être elles-mêmes **dans** une classe de caractères. Par exemple, pour chercher un caractère de ponctuation seul, il faut écrire `[[:punct:]]`.
- Java et  Python n'acceptent pas les POSIX entre crochets; mais Perl les accepte. On peut de même faire une recherche en utilisant les POSIX entre crochets dans LibreOffice  ou encore  TexStudio
- Les raccourcis (commençant par `\`) sont communément reconnus. Certains langages en utilisent également d'autres.




### Quantificateurs

- Les *quantificateurs* se placent après un caractère ou un groupement de caractères pour indiquer le nombre de répétitions de ce caractère ou de ce groupement de caractères.
-  *groupement*: ensemble "capturé", au sein duquel peut se trouver l'opérateur OU, et sur lequel peuvent porter les quantifieurs. Cet ensemble est conservé en mémoire et peut être réutilisé plus tard (cf *infra*).
Exemple: `m(o|a|e)t` = `mot|mat|met`; `m(ou|iau)le` = `moule|miaule`



|Quantificateur|Explication|
|-- |-- |
|`{min,max}`|le nombre de répétitions varie entre la valeur minimale et la valeur maximale incluses|
|`{min,}`| le nombre de répétitions varie entre la valeur minimale incluse et l'infini|
|`{,max}`| le nombre de répétitions varie entre 0 et la valeur maximale incluse|
|`{nombre}`| le nombre de répétitions correspond au nombre marqué entre les accolades|
|`*`|0, 1 ou plusieurs répétitions (équivalent de `{0,}`|
|`?`|0 ou 1 répétition (équivalent de `{,1}`|
|`+`|1 ou plusieurs répétitions (équivalent de `{1,}`|



### Ancres et mise en place du texte

|expression|équivalent|
|--|-- |
|`\b`|début ou fin de mot|
|`\B`|au milieu d'un mot (inverse de `\B`)|
|`\n`|fin de ligne|
|`\r`|retour charriot (saut de paragraphe)|
|`\t`|tabulation|
`\f`| pagebreak|
| `^`|début de ligne|
|`$`|fin de chaine/fin de ligne|


**nb**: 
- la différence entre fin de ligne et retour charriot n'apparait pas dans le texte brut; en revanche, elle joue un rôle dans les traitements de texte WYSIWYG.
- dans Libreoffice, `$` indique la fin de ligne,  `\n`  le saut de paragraphe. 



### Groupement, captures et références arrières (*backreferences*)


- les groupements (voir *supra*) gardent en mémoire l'élément mis entre parenthèses. Celui-ci peut ensuite être rappelé,  dans la regex, par `\1, \2` et  dans la fonction de remplacement, par `$1, $2` ou `\1, \2` selon les langages.
-  Le chiffre permet de se référer au groupement, dans l'ordre d'apparition dans la regex;  c'est ce que l'on appelle les références arrières (*backreferences*). 

 **Exemples**

1.  `(.)\1` cherche n'importe quel caractère, gardé en mémoire dans le groupement 1, suivi du même caractère (aa, bb, deux espaces à la suite, etc).
2. `(\d{2})\/(\d{2})` cherche, par exemple, l'expression de la date selon le format `jour/mois`, qui peut être remplacée par `$2-$1` pour obtenir mois-jour.


<!--**nb** Il est également possible de donner un nom aux groupements pour les rappeler ensuite par ce nom-->


### Les "flags" (drapeaux, modificateurs de recherche)

- Les flags, ou drapeaux, permettent de modifier la façon dont fonctionnent les recherches
- nous avons déjà évoqué le drapeau "u" qui permet d'inclure les caractères unicode, par exemple dans la classe `\w`
- autre utilisation: rendre les opérateur "paresseux". Exemple: l'expression `".*"` sélectionnera le plus grand texte possible, comme `"du texte entre guillemets" et "encore un autre"`. Pour ne sélectionner que la première partie entre guillemets, il faut mettre le flag "ungreedy" (`U`)
- autre possibilité: enlever le flag "global" (`g`) pour ne trouver que la première occurrence

### Les recherches avant et arrière (*lookaround*) 

Ces fonctions   permettent de préciser, sans les conserver en mémoire, les éléments qui précèdent (*lookahead*, recherche avant) ou qui suivent (*lookbehind*, recherche arrière) les motifs recherchés. Elles peuvent être positives (suivre ou précéder) ou négatives (ne pas suivre ni précéder).

|Fonction|Expression|Exemple|
|-- |-- |-- |
|Recherche avant positive|`(?=x)`|`c(?=d)`: c suivi de d|
|Recherche avant négative|`(?!x)`|`c(?!d)`: c non suivi de d|
|Recherche arrière positive|`(?<=x)`|`(?<=d)c`: c précédé de d|
|Recherche arrière négative|`(?<!x)`|`(?<!d)c`: non précédé de d|

- Attention: même s'il y a des parenthèse, ce n'est pas conservé en mémoire!

- Les recherches avant et arrière servent notamment à extraire des données entre balises.
Pour sélectionner le texte entre balises dans l'exemple suivant: `<balise>contenu de la balise</balise>`, il faut écrire `(?<=<balise>).*(?=<\/balise>)` 


**nb**
Il est également possible  d'écrire une structure conditionnelle (*if then else*) en utilisant la recherche avant. Voir par exemple le tutoriel [ici](https://stormimon.developpez.com/dotnet/expressions-regulieres/#L3-9)

## Pour aller plus loin

1. Il existe sous linux un outil en ligne de commande,  `sed`, qui permet de modifier des fichiers en leur appliquant des recherches et des substitutions formulées en regex. 

Vous trouverez par exemple un tutoriel  [ici](https://fr.linux-console.net/?p=14620) 

2. Un article évoquant notamment l'utilisation possible des regex par les historiens : Sébastien de Valeriola, *L’ordinateur au service du dépouillement de sources historiques*, [ici](https://www.cairn.info/revue-histoire-et-mesure-2020-2-page-171.htm&wt.src=pdf)

3. Un blog exposant comment extraire sous forme de tableau les données d'un texte, au moyen des regex: [ici](https://programminghistorian.org/fr/lecons/comprendre-les-expressions-regulieres)
