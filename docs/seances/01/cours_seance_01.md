---
marp: true
theme: tech-info
title: "Séance 1 — Modules built-in et personnels"
paginate: true
header: "Labo Tech Info 2 — Séance 1 [Sylvain Huraux - HE2B - ISIB](mailto:shuraux@he2b.be)"
footer: "[← Retour à l'accueil](../../index.html)"
---

# Séance 1

Modules *built-in* et modules personnels

[→ Quiz](quiz_seance_01.html)
[→ Exercices](exercices_seance_01.html)

---

## Objectifs de la séance

- Passer de Thonny (TI1) à PyCharm pour le labo
- Comprendre ce qu'est un *module* et comment l'`importer`
- Utiliser des modules de la bibliothèque standard
- Créer et importer ses propres modules (fichiers `.py`)
- Relier brièvement à `if __name__ == "__main__"` (déjà vu en TI1)

---

## Fil du laboratoire

Sept séances, dans cet ordre :

1. Modules (*built-in* et personnels) (aujourd'hui)
2. Exceptions
3. Manipulation de fichiers (txt, JSON, csv) + `input`
4. numpy et ndarray
5. Pandas (bases)
6. Pandas (suite)
7. Matplotlib

On commence par l'outil et l'`import`. Le reste viendra ensuite.

---

## Pourquoi quitter Thonny ?

En TI1, *Thonny* suffisait : éditer et exécuter au même endroit, interface simple.

En LTI2 on ira vers des projets plus structurés (plusieurs fichiers, modules, bibliothèques). *PyCharm* est un *IDE* plus complet, mieux adapté à cette suite.

Thonny n'est pas « faux » : on change d'outil parce que le travail évolue.

---

## PyCharm : l'essentiel

*PyCharm* (édition Community) : éditeur, explorateur de projet, bouton Run, console, terminal.

- **New Project** / **Open** : un dossier de travail
- *New* → *Python File* : créer un `.py`
- *Run* (▶ ou clic droit) : exécuter ; sortie et erreurs dans la console

Comme Thonny : on édite et on exécute au même endroit. Aujourd'hui : être autonome pour les exos multifichiers.

---

## Qu'est-ce qu'un module ?

Un *module* = un fichier `.py` (ou une bibliothèque) dont on réutilise le code.

```python
import math

print(math.sqrt(16))
```

- `import` charge le module
- on accède aux noms via `math.nom`

Sans module : tout dans un seul fichier. Avec modules : découper et réutiliser.

---

## Formes d'`import`

```python
import math
from math import sqrt, pi
import math as m
```

- `import math` : tout le module, préfixe `math.`
- `from math import sqrt` : importer des noms précis
- `as` : donner un alias (`m.sqrt(...)`)

Choisir la forme la plus lisible pour le script.

---

## Modules *built-in* / stdlib

La bibliothèque standard fournit déjà beaucoup d'outils. Exemples utiles en labo :

- `math` : fonctions mathématiques
- `random` : tirages aléatoires
- `json` : structures en mémoire (fichier `.json` : séance 3)
- `pathlib` : chemins de fichiers

Ce ne sont pas des « extras » à installer : ils viennent avec Python.

---

## Exemple : `math` et `random`

```python
import math
import random

angle = math.radians(90)
print(math.sin(angle))

print(random.randint(1, 6))
```

On combine plusieurs modules dans le même script.
Chaque module a sa doc et ses fonctions.

---

## Modules personnels

Vous pouvez créer vos propres modules : un fichier `.py` à côté de votre script.

`utils.py` :

```python
def double(n: int) -> int:
    return n * 2
```

`main.py` :

```python
from utils import double

print(double(21))
```

Même idée que `import math`, mais le code est le vôtre.

---

## Plusieurs fichiers dans PyCharm

Dans le projet :

- `utils.py` : fonctions réutilisables
- `main.py` (ou `app.py`) : point d'entrée qui importe `utils`

Les deux fichiers doivent être dans le même dossier (pour commencer), ou dans un paquet plus tard.

Run sur `main.py` : c'est lui qui tire les fils.

---

## `if __name__ == "__main__"` (rappel)

Vu en TI1. Utile dès qu'on importe un module perso :

```python
# utils.py
def double(n: int) -> int:
    return n * 2


if __name__ == "__main__":
    print(double(2))  # seulement si on lance utils.py directement
```

- importé depuis ailleurs : le `if` ne s'exécute pas
- lancé directement : le bloc de test / démo s'exécute

Rappel bref, pas le cœur de la séance.

---

## Script avec `main()` + import

```python
# app.py
from utils import double


def main() -> None:
    print(double(21))


if __name__ == "__main__":
    main()
```

Structure déjà vue en TI1 ; aujourd'hui elle sert à organiser un projet multifichiers.

---

## Alias et bons réflexes

```python
import math as m
from pathlib import Path
```

- alias court si le module revient souvent (`np`, `pd` plus tard)
- `from … import …` pour 1-2 noms vraiment utilisés
- éviter `from module import *` (lisibilité, collisions de noms)

---

## Vers les séances suivantes

Aujourd'hui : `import` stdlib + modules perso dans PyCharm.

Ensuite :

- **S2** : exceptions (`try` / `except`), y compris `ImportError`
- **S3** : fichiers txt / JSON / csv + `input` (réinvestissement de `json`, `pathlib`)
- **S4+** : numpy, pandas, matplotlib (autres `import`, paquets tiers)

---

## Conclusion de la séance

- LTI2 se fait dans PyCharm (TI1 : Thonny)
- Un module se charge avec `import` / `from … import …` / `as`
- Stdlib : `math`, `random`, `json`, `pathlib`, …
- Modules perso : plusieurs `.py` dans le même projet
- Suite : exceptions (séance 2)

[→ Quiz](quiz_seance_01.html) [→ Exercices](exercices_seance_01.html)
