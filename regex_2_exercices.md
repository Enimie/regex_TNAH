# Cours 2 - Exercices

###  Les caractères unicodes (suite):

 copier dans [regex2](https://regex101.com/) les émoticônes suivantes:
`😀😖😩`

Le premier a pour encodage `U+1F600`; le second a pour encodage `U+1F616`; le troisième `U+1F629`.
 Pour rechercher un caractère unicode par son encodage, il faut taper `\x{code du caractère}`

- Choisir un émoticône et le sélectionner par une regex
- Trouver un moyen pour sélectionner les trois à la fois

- Coller les carcatères syriens suivants et chercher comment les sélectionner: 
```
ܚܟܤ

```

### Exercices

Pour ce cours, les exercices se font sur le texte suivant, à copier dans [regex2](https://regex101.com/)

```
Le hareng saur (1872)

Il était un grand mur blanc - nu, nu, nu,
Contre le mur une échelle - haute, haute, haute,
Et, par terre, un hareng saur - sec, sec, sec.

Il vient, tenant dans ses mains - sales, sales, sales,
Un marteau lourd, un grand clou - pointu, pointu, pointu,
Un peloton de ficelle - gros, gros, gros.

alors il monte à l'échelle - haute, haute, haute,
Et plante le clou pointu - toc, toc, toc,
Tout en haut du grand mur blanc - nu, nu, nu.

Il laisse aller le marteau - qui tombe, qui tombe, qui tombe,
Attache au clou la ficelle - longue, longue, longue,
et, au bout, le hareng saur - sec, sec, sec.

Il redescend de l'échelle - haute, haute, haute,
l'emporte avec le marteau - lourd, lourd, lourd,^[une note de bas de page rédigée en markdown]
Et puis, il s'en va ailleurs - loin, loin, loin.

Et, depuis, le hareng saur - sec, sec, sec,
Au bout de cette ficelle - longue, longue, longue,
Très lentement se balance - toujours, toujours, toujours.

J'ai composé cette histoire - simple, simple, simple,
pour mettre en fureur les gens - graves, graves, graves,
Et amuser les enfants - petits, petits, petits.

Charles Cros (1842-1888)

Source sur "Le hareng saur": "Wikipédia"  https://fr.wikipedia.org/wiki/Le_Hareng_saur
```

## Remise en jambe regex


- Trouver l'auteur du poème
- Trouver la date du poème, entre parenthèses
- Trouver l'url
- Sélectionner uniquement la première partie de l'url  (jusqu'au `/`)
- Sélectionner `saur` et `sec`,  puis `haut` et `haute`


### Ancres et  mise en place du texte


- Trouver tous les mots terminant par la lettre `c` 
- Trouver tous les `c` au milieu d'un mot
- Sélectionner les mots de trois lettres
- Vérifier qu'il y a bien une majuscule en début de chaque vers


### Groupements, captures et références arrières (*backreference*)

- Repérer les mots ou expressions répétés trois fois. 

Mettons à présent le texte en LaTeX. Pour cela, à chacune des opérations suivantes, copier-coller le texte sur lequel ont eu lieu les substitutions pour conserver les modifications.

- Mettre l'url dans une commande `\url` (attention, ne pas prendre l'espace)
- Mettre le nom de l'auteur, qui est au format "Prénom Nom",  dans la commande `\auteur{Nom}{Prénom}`
- Remplacer la note de bas de page rédigée au format markdown (`[^ texte de la note]`) par une  `\footnote{texte}`
- Remplacer les guillemets ("") par la commande `\enquote{}` 
+ Mettre le titre dans la commande \section{}`, sans les parenthèses
- Sélectionner les vers; ajouter `&` à la fin des vers.
- À la fin des strophes, il faut `\&` au lieu de `&`
- Au début de chaque strophe, il faut `\stanza`
- Mettre `\beginnumbering` avant la première commande `\stanza`
- Trouver le dernier `\&` pour mettre `endnumbering` après la dernière strophe

