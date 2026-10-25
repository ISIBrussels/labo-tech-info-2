---
marp: true
theme: tech-info
title: "Séance 1 — Manipulation de fichiers (txt, JSON, csv)"
paginate: true
header: "Labo Tech Info 2 — Séance 1 [Sylvain Huraux - HE2B - ISIB](mailto:shuraux@he2b.be)"
footer: "[← Retour à l'accueil](../../index.html)"
---

# Séance 1

Manipulation de fichiers (txt, JSON, csv)

[→ Quiz](quiz_seance_01.html)
[→ Exercices](exercices_seance_01.html)

---

## Objectifs de la séance

- Passer de Thonny (TI1) à PyCharm pour le labo
- Ouvrir un projet, lancer un script, lire une erreur
- Découvrir `input` : saisie clavier, toujours une `str` ; one-liners classiques
- Lire et écrire des fichiers **txt**, **JSON**, **csv**
- Enchaîner saisie et fichiers dans de petits scripts

---

## Fil du laboratoire

Sept séances, dans cet ordre :

1. Manipulation de fichiers (txt, JSON, csv) + `input` (aujourd'hui)
2. Exceptions
3. numpy et ndarray
4. Pandas (bases)
5. Pandas (suite)
6. Modules (*built-in* et personnels)
7. Matplotlib

On commence par l'outil, la saisie, puis les fichiers. Le reste viendra ensuite.

---

## Pourquoi quitter Thonny ?

En TI1, *Thonny* suffisait : éditer et exécuter au même endroit, interface simple.

En LTI2 on ira vers des projets plus structurés (plusieurs fichiers, modules, bibliothèques). *PyCharm* est un *IDE* plus complet, mieux adapté à cette suite.

Thonny n'est pas « faux » : on change d'outil parce que le travail évolue.

---

## PyCharm : vue d'ensemble

*PyCharm* (édition Community, gratuite) regroupe notamment :

- un éditeur de code (coloration, indentation, suggestions)
- un explorateur de fichiers / projet
- un bouton pour lancer le script
- une zone de sortie (console) pour `print` et les erreurs
- un terminal intégré

Comme Thonny : on édite et on exécute au même endroit. La fenêtre est simplement plus riche.

---

## Créer ou ouvrir un projet

Un *projet* PyCharm = un dossier de travail (vos `.py` et, plus tard, d'autres fichiers).

- **New Project** : choisir un dossier vide, créer le projet
- **Open** : ouvrir un dossier déjà existant (ex. exercices du labo)

Conseil : un dossier clair par séance ou par série d'exercices, pas des fichiers éparpillés sur le Bureau.

---

## Premier fichier dans le projet

Dans l'explorateur à gauche :

- clic droit sur le dossier du projet → *New* → *Python File*
- nommer par ex. `hello.py` (PyCharm ajoute `.py` si besoin)

Écrire :

```python
print("hello from pycharm")
```

Enregistrer (`Ctrl+S` / `Cmd+S`). Le fichier apparaît dans l'arbre du projet.

---

## Lancer un script

Plusieurs façons équivalentes au début :

- clic droit sur le fichier → *Run 'hello'*
- ou bouton vert ▶ en haut à droite (après un premier lancement)
- raccourci : `Shift+F10` (souvent)

La sortie de `print` apparaît dans la console en bas (*Run*).

C'est l'équivalent du bouton « Run » de Thonny, branché sur le fichier courant.

---

## Terminal et erreurs

PyCharm inclut un *Terminal* (onglet en bas) : utile plus tard pour `pip`, chemins.

Quand le programme plante :

1. la console *Run* affiche le message (type, fichier, ligne)
2. l'éditeur souligne souvent la zone suspecte
3. un clic sur le numéro de ligne dans la trace ouvre l'endroit concerné

Comme en TI1 : lire le type d'erreur et la ligne avant de tout réécrire.

---

## PyCharm : gestes du jour

À retenir pour la suite du labo :

- travailler dans un *projet* (dossier), pas un fichier isolé « perdu »
- *Run* pour exécuter le script courant
- console *Run* pour la sortie et les messages d'erreur
- terminal / console Python seulement si utile

Aujourd'hui : être autonome pour les exercices (saisie + fichiers).

---

## Rappel TI1 (ciblé)

On ne refait pas TI1. Juste le socle utile pour `input` et les fichiers :

- types : `int`, `float`, `bool`, `str`
- casting : `int(...)`, `float(...)`, `str(...)`
- `if` / `elif` / `else`, boucles `while` / `for`
- listes / dictionnaires (surtout pour JSON)
- fonctions, et souvent un `main()` déjà vu en séance 6

Si une notion manque : on la rappelle au moment où l'exercice l'exige.

---

## `input` : écouter l'utilisateur

```python
name = input("Votre prénom : ")
print(f"Bonjour, {name}.")
```

- affiche le message (la *invite*)
- attend que l'utilisateur tape puis valide (`Entrée`)
- renvoie la saisie : **toujours une `str`**

`print` sort ; `input` entre.

---

## One-liners classiques

```python
name = input("Prénom : ")
age = int(input("Âge : "))
price = float(input("Prix : "))
print(f"{name} a {age} ans.")
```

- `int(input(...))` / `float(input(...))` : saisie + conversion sur une ligne
- `print(f"...")` : affichage formaté (rappel *f-string* TI1)
- Pour l'instant : saisie « raisonnable » ; mauvaises saisies → séance exceptions

---

## Du clavier au fichier

Parfois on demande une valeur au clavier. Souvent, les données sont déjà dans un fichier.

Aujourd'hui : lire et écrire trois formats courants en labo.

- **txt** : texte ligne par ligne
- **JSON** : structures (`dict` / `list`) sérialisées
- **csv** : tableaux (lignes + colonnes)

`input` reste utile pour un chemin, un choix de menu, un paramètre.

---

## Fichier vs chemin

Un *fichier* est sur le disque. Un *chemin* dit où le trouver.

```python
path = "data/notes.txt"
```

Modes courants à l'ouverture :

- `r` : lire (défaut)
- `w` : écrire (écrase si le fichier existe)
- `a` : ajouter à la fin

Encodage recommandé : **UTF-8**.

---

## `with open(...) as f`

```python
with open("message.txt", "r", encoding="utf-8") as f:
    text = f.read()
print(text)
```

- `with` ferme le fichier proprement à la fin du bloc
- on travaille avec `f` (le fichier ouvert)
- préférer cette forme à `open` / `close` manuels

---

## Fichiers texte (txt)

```python
with open("lignes.txt", "r", encoding="utf-8") as f:
    for line in f:
        print(line.strip())
```

Utile aussi :

- `f.read()` : tout le contenu
- `f.readlines()` : liste de lignes
- `f.write("…\n")` en mode `"w"` ou `"a"`

Itérer sur `f` : lecture ligne à ligne, simple et claire.

---

## Écrire un txt

```python
name = input("Prénom : ")
with open("bonjour.txt", "w", encoding="utf-8") as f:
    f.write(f"Bonjour, {name}.\n")
```

Enchaînement typique du jour : saisie → écriture dans un fichier.

Attention au mode `"w"` : il écrase le contenu précédent.

---

## JSON : structures en fichier

JSON encode des données proches des `dict` / `list` de TI1.

```python
import json

with open("etudiant.json", "r", encoding="utf-8") as f:
    data = json.load(f)
print(data["prenom"])
```

- `json.load(f)` : fichier → objet Python
- `json.dump(obj, f)` : objet Python → fichier
- `import json` : usage pragmatique ; formalisation des modules en séance 6

---

## Écrire un JSON

```python
import json

person = {"prenom": "Ada", "age": 36}
with open("person.json", "w", encoding="utf-8") as f:
    json.dump(person, f, ensure_ascii=False, indent=2)
```

- `ensure_ascii=False` : accents conservés
- `indent=2` : fichier lisible pour un humain

On retrouve `dict` / `list` côté Python, JSON côté disque.

---

## CSV : lignes et colonnes

```python
import csv

with open("notes.csv", "r", encoding="utf-8", newline="") as f:
    reader = csv.DictReader(f)
    for row in reader:
        print(row["nom"], row["note"])
```

- module `csv` de la bibliothèque standard
- `DictReader` : chaque ligne → dictionnaire (clés = en-têtes)
- pandas viendra plus tard pour l'analyse tabulaire

---

## Écrire un CSV

```python
import csv

rows = [{"nom": "Ada", "note": "18"}, {"nom": "Alan", "note": "16"}]
with open("notes.csv", "w", encoding="utf-8", newline="") as f:
    writer = csv.DictWriter(f, fieldnames=["nom", "note"])
    writer.writeheader()
    writer.writerows(rows)
```

`newline=""` : recommandé sous Python pour le module `csv` (comportement portable).

---

## Erreurs fréquentes (aperçu)

Sans tout gérer aujourd'hui, reconnaître les messages :

- fichier introuvable → `FileNotFoundError`
- JSON invalide → `json.JSONDecodeError`
- conversion `int(input(...))` impossible → `ValueError`

Lire le type et la ligne (comme en TI1). La gestion propre avec `try` / `except` : **séance 2**.

---

## Bonnes pratiques (jour 1)

- projet PyCharm clair ; données dans un sous-dossier (`data/…`)
- toujours `encoding="utf-8"` et `with open(...)`
- invites `input` explicites ; one-liners lisibles
- scripts courts : une tâche claire (lire, filtrer, réécrire)
- ne pas encore « blinder » chaque erreur : ce sera pour S2

---

## Conclusion de la séance

- LTI2 se fait dans PyCharm (TI1 : Thonny)
- `input` lit au clavier et renvoie toujours une `str` ; one-liners utiles
- txt / JSON / csv : lire et écrire avec `with open(...)`
- `json` et `csv` : premiers `import` pragmatiques
- Suite : exceptions (séance 2), pour rendre ces scripts robustes

[→ Quiz](quiz_seance_01.html) [→ Exercices](exercices_seance_01.html)
