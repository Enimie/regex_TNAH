# Cours 3 - Exercices

## Les fonctions de préanalyse et de postanalyse (*lookaround*) 

Copier le texte suivant:

```
Testons les fonctions de lookaround avec ce texte.

Une phrase(sans intérêt en soi)où il manque des espaces avant ou après la ponctuation:rétablissons les!mais attention aux commandes latex\footnote{elles commencent par un antislash}.Voilà,c'est fait.Peut-on continuer?Sans doute.

un lien:https://regex101.com/
```

**exercices**


- Sélectionner le nom du site, sans les slash avant et après, et le remplacer par `monsite.org`
- Ajouter les espaces oubliés avant ou après des signes de ponctuation.
- Tester la ponctuation à la fin de la `\footnote`.  Rajouter le point manquant

## Nettoyer et transformer un texte récupéré à partir d'un pdf ou d'une transciption OCR

### Nettoyer un texte sur LibreOffice

Copier le texte par OCR (reconnaissance optique de caractère) [ici](https://gallica.bnf.fr/ark:/12148/bpt6k96742375/f7.item)



1. enlever les tirets de césure
2. repérer la façon dont sont traités les paragraphes: deux retours charriots -> les remplacer par `\n` (qui devient un saut de paragraphe)
3. supprimer les retours à la ligne (retour charriot) excédentaires
4. supprimer les espaces avant les sauts de paragraphe (`\s$` remplacés par rien)

### Transformer en tableur une liste 

-  copier la liste des membres souscripteurs p.7-9 [ici](https://gallica.bnf.fr/ark:/12148/bpt6k53270117/f17.vertical)

**nettoyage**
- enlever titre
- supprimer les fins de ligne qui ne sont pas des fin d'entrée: remplacer `(?<![;,:] )\n` par rien, puis `\n[\d[:lower:]]` (celles qui restaient)
- uniformiser les fins d'entrée  par un saut de paragraphe sans ponctuation: ` [,;:] \n` remplacé par `\n` puis `[,;:] ?$` a remplaer par rien

**le but est d'obtenir trois colonnes (séparées par une tabulation): Nom, raison sociale, adresse**


- séparer les adresses par une tabulation
	+ `, (\d)` remplacé par `\t$1`
	+  tester par un  collage spécial dans un tableur (choisir "Unformatted text").
	+ trouver les adresses qui n'ont pas de numéro 
	+ Chercher manuellement les cas d'adresse manquante (lignes sans tabulation)

- séparer la raison sociale par une tabulation
	+  Commencer par les raisons sociales entre virgules `(^[^\t]+), ([^\t]+)` -> `$1 \t $2` 
	+ Raisons sociales entre parenthèses, désormais suivies d'une tabulation. 
	+ Ne pas prendre en compte les initiales (majuscules seules ou suivies d'un point) ni les particules (en minuscules). Certaines tabulations sont précédées d'un espace -> `\([A-Z][^.]+\) ?(?=\t)`. Utiliser les références arrières dans le remplacement.

- Pour ceux/celles qui n'ont pas de raison sociale: il faut deux tabulation à la suite pour créer une colonne vide. 
	+ trouver les lignes avec une seule tabulation: `^[^\t]+\t[^\t]+$` ; créer deux groupements, qui se retrouveront avant et après la double tabulation.


5.  verifier dans le tableau et ajuster



