---
marp: true
theme: tech-info
title: "Séance 3 — Manipulation de fichiers (txt, JSON, csv) + input"
paginate: true
header: "Labo Tech Info 2 — Séance 3 [Sylvain Huraux - HE2B - ISIB](mailto:shuraux@he2b.be)"
footer: "[← Retour à l'accueil](../../index.html)"
---

# Séance 3

Manipulation de fichiers (txt, JSON, csv) + `input`

[→ Quiz](quiz_seance_03.html)
[→ Exercices](exercices_seance_03.html)

---

## Objectifs de la séance

- Découvrir `input` : saisie clavier, toujours une `str` ; one-liners classiques
- Lire et écrire des fichiers **txt**, **JSON**, **csv**
- Réinvestir `import` (S1) et `try` / `except` (S2)
- Enchaîner saisie et fichiers dans de petits scripts (PyCharm)

---

## Fil du laboratoire

1. Modules (*built-in* et personnels)
2. Exceptions
3. Manipulation de fichiers + `input` (aujourd'hui)
4. Numpy : tableaux ndarray
5. Pandas : series et dataframe (bases)
6. Pandas : series et dataframe (suite)
7. Matplotlib

---

## Rappel TI1 (ciblé)

On ne refait pas TI1. Socle utile pour `input` et les fichiers :

- types et casting : `int(...)`, `float(...)`, `str(...)`
- `if` / boucles ; listes / dictionnaires (surtout pour JSON)
- `main()` déjà vu ; modules et exceptions : S1-S2

---

## `input` : écouter l'utilisateur

```python
name = input("Votre prénom : ")
print(f"Bonjour, {name}.")
```

- affiche l'*invite*, attend `Entrée`, renvoie la saisie
- **toujours une `str`** (même si on tape `20`)

`print` sort ; `input` entre.

---

## One-liners classiques

```python
name = input("Prénom : ")
age = int(input("Âge : "))
price = float(input("Prix : "))
print(f"{name} a {age} ans.")
```

- `int(input(...))` / `float(input(...))` : saisie + conversion
- `print(f"...")` : affichage formaté
- Conversion impossible → `ValueError` (S2 : `try` / `except`)

---

## Du clavier au fichier

Parfois on demande une valeur au clavier. Souvent, les données sont déjà dans un fichier.

Aujourd'hui : trois formats courants en labo.

- **txt** : texte ligne par ligne
- **JSON** : structures (`dict` / `list`) sérialisées
- **csv** : tableaux (lignes + colonnes)

`input` reste utile pour un chemin, un choix, un paramètre.

---

## Fichier vs chemin

```python
from pathlib import Path

path = Path("data/notes.txt")
```

Modes courants :

- `r` : lire (défaut)
- `w` : écrire (écrase si le fichier existe)
- `a` : ajouter à la fin

Encodage recommandé : **UTF-8**. `pathlib` : déjà croisé en S1.

---

## `with open(...) as f`

```python
with open("message.txt", "r", encoding="utf-8") as f:
    text = f.read()
print(text)
```

- `with` ferme le fichier proprement à la fin du bloc
- préférer cette forme à `open` / `close` manuels

---

## Fichiers texte (txt)

```python
with open("lignes.txt", "r", encoding="utf-8") as f:
    for line in f:
        print(line.strip())
```

Utile aussi : `f.read()`, `f.readlines()`, `f.write("…\n")` en mode `"w"` ou `"a"`.

---

## Écrire un txt (avec saisie)

```python
name = input("Prénom : ")
with open("bonjour.txt", "w", encoding="utf-8") as f:
    f.write(f"Bonjour, {name}.\n")
```

Enchaînement typique : saisie → écriture. Attention au mode `"w"` : il écrase.

---

## JSON : structures en fichier

```python
import json

with open("etudiant.json", "r", encoding="utf-8") as f:
    data = json.load(f)
print(data["prenom"])
```

- `json.load` / `json.dump` : fichier ↔ objet Python
- `import json` : réinvestissement S1 (là : plutôt en mémoire ; ici : I/O)

---

## Écrire un JSON

```python
import json

person = {"prenom": "Ada", "age": 36}
with open("person.json", "w", encoding="utf-8") as f:
    json.dump(person, f, ensure_ascii=False, indent=2)
```

`ensure_ascii=False` : accents conservés. `indent=2` : lisible.

---

## CSV : lignes et colonnes

```python
import csv

with open("notes.csv", "r", encoding="utf-8", newline="") as f:
    reader = csv.DictReader(f)
    for row in reader:
        print(row["nom"], row["note"])
```

`DictReader` : chaque ligne → dictionnaire (clés = en-têtes). Pandas : plus tard (S5-S6).

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

`newline=""` : recommandé avec le module `csv`.

---

## Erreurs : réinvestir S2

```python
try:
    age = int(input("Âge : "))
except ValueError:
    print("Entrez un entier.")

try:
    with open("data.json", "r", encoding="utf-8") as f:
        data = json.load(f)
except FileNotFoundError:
    print("Fichier introuvable.")
except json.JSONDecodeError:
    print("JSON invalide.")
```

Aujourd'hui : scripts utiles **et** robustes.

---

## Bonnes pratiques

- données dans un sous-dossier (`data/…`) ; `encoding="utf-8"` ; `with open(...)`
- invites `input` explicites ; one-liners lisibles
- `try` / `except` sur saisie et I/O prévisibles
- scripts courts : une tâche claire

---

## Conclusion de la séance

- `input` renvoie toujours une `str` ; one-liners utiles
- txt / JSON / csv avec `with open(...)`
- `json` / `csv` / `pathlib` : modules S1 en situation I/O
- `try` / `except` (S2) pour ne pas planter
- Suite : Numpy : tableaux ndarray (séance 4)

[→ Quiz](quiz_seance_03.html) [→ Exercices](exercices_seance_03.html)
