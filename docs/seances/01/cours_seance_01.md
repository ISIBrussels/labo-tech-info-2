---
marp: true
theme: tech-info
title: "Séance 1 — Fonction input"
paginate: true
header: "Labo Tech Info 2 — Séance 1 [Sylvain Huraux - HE2B - ISIB](mailto:shuraux@he2b.be)"
footer: "[← Retour à l'accueil](../../index.html)"
---

# Séance 1

Fonction `input`

[→ Quiz](quiz_seance_01.html)
[→ Exercices](exercices_seance_01.html)

---

## Objectifs de la séance

- Passer de Thonny (TI1) à PyCharm pour le labo
- Ouvrir un projet, lancer un script, lire une erreur
- Rappeler le socle utile de TI1 (sans tout rejouer)
- Découvrir `input` : saisie clavier, toujours une `str`
- One-liners classiques : `int(input(...))`, `float(input(...))`, `print(f"...")`
- Enchaîner `input` + casting pour de petits dialogues

---

## Fil du laboratoire

Sept séances, dans cet ordre :

1. `input` (aujourd'hui) + prise en main de PyCharm
2. Modules (*built-in* et personnels)
3. Exceptions
4. Fichiers (txt, json, csv)
5. NumPy
6. Pandas
7. Matplotlib

On commence calmement : outil + saisie. Le reste viendra ensuite.

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

## Terminal intégré

PyCharm inclut un *Terminal* (onglet en bas).

On peut y faire comme en ligne de commande :

```bash
python hello.py
```

Utile plus tard pour `pip`, chemins, commandes hors du bouton Run.

Pour démarrer : le bouton ▶ suffit. Le terminal reste disponible quand on en a besoin.

---

## Console Python (REPL) dans PyCharm

Besoin de tester une expression sans écrire un fichier ?

- *Tools* → *Python Console* (ou onglet *Python Console*)
- ou dans le terminal : `python`, puis instructions une à une

Même idée que le shell de Thonny / le REPL vu en TI1 : expérimenter, puis reporter le code stable dans un script `.py`.

---

## Où voir les erreurs ?

Quand le programme plante :

1. la console *Run* affiche le message (type, fichier, ligne)
2. l'éditeur souligne souvent la zone suspecte
3. un clic sur le numéro de ligne dans la trace ouvre l'endroit concerné

Exemple :

```text
NameError: name 'prin' is not defined
```

Comme en TI1 : lire le type d'erreur et la ligne avant de tout réécrire.

---

## PyCharm : gestes du jour

À retenir pour la suite du labo :

- travailler dans un *projet* (dossier), pas un fichier isolé « perdu »
- *Run* pour exécuter le script courant
- console *Run* pour la sortie et les messages d'erreur
- terminal / console Python seulement si utile

On approfondira l'IDE au fil des séances (modules, paquets…). Aujourd'hui : être autonome pour les exercices.

---

## Rappel TI1 (ciblé)

On ne refait pas TI1. Juste le socle utile pour `input` :

- types : `int`, `float`, `bool`, `str`
- casting : `int(...)`, `float(...)`, `str(...)`
- `if` / `elif` / `else`, boucles `while` / `for`
- fonctions, et souvent un `main()` déjà vu en séance 6

Si une notion manque : on la rappelle au moment où l'exercice l'exige.

---

## `print` : parler à l'utilisateur

```python
print("Bonjour")
print("Résultat :", 42)
```

- affiche des informations à l'écran
- n'attend pas de réponse

Utile pour guider, confirmer, afficher un résultat.

---

## `input` : écouter l'utilisateur

```python
name = input("Votre prénom : ")
print(f"Bonjour, {name}.")
```

- affiche le message (la *invite*)
- attend que l'utilisateur tape puis valide (`Entrée`)
- renvoie la saisie

`print` sort ; `input` entre.

---

## Toujours une `str`

```python
age_text = input("Âge : ")
print(type(age_text))   # <class 'str'>
```

Même si on tape `20`, `input` renvoie la chaîne `"20"`, pas l'entier `20`.

Conséquence : pour calculer, il faudra convertir (casting vu en TI1).

---

## `input` + casting

```python
age_text = input("Âge : ")
age = int(age_text)
print(f"Dans 10 ans : {age + 10}")
```

Deux étapes : lire (toujours une `str`), puis convertir.
On peut aussi le faire en une seule instruction.

---

## One-liners classiques

Formules très fréquentes dès qu'on combine `input` et le casting TI1 :

```python
name = input("Prénom : ")
age = int(input("Âge : "))
price = float(input("Prix : "))
print(f"{name} a {age} ans.")
```

- `int(input(...))` / `float(input(...))` : saisie + conversion sur une ligne
- `print(f"...")` : affichage formaté (rappel *f-string* TI1)
- Pas de compréhensions de listes ni d'astuces « golf » : on reste lisible

---

## Attention aux conversions

```python
int("20")      # OK → 20
int("20.5")    # erreur (ValueError)
float("20.5")  # OK → 20.5
int("vingt")   # erreur
```

Pour l'instant : on suppose une saisie « raisonnable ».
Gérer proprement les mauvaises saisies : séance sur les exceptions.

---

## Petit dialogue

```python
def main() -> None:
    name = input("Prénom : ")
    city = input("Ville : ")
    print(f"{name} habite à {city}.")


if __name__ == "__main__":
    main()
```

Enchaîner plusieurs `input`, puis un message de synthèse.
La structure `main()` / `if __name__ == "__main__"` : déjà vue en TI1 ; on la réutilise.

---

## Menu texte simple

```python
print("1. Dire bonjour")
print("2. Quitter")
choice = input("Votre choix : ")

if choice == "1":
    print("Bonjour !")
elif choice == "2":
    print("Au revoir.")
else:
    print("Choix inconnu.")
```

`input` alimente des conditions (et plus tard des boucles) : bases des programmes interactifs.

---

## Boucle + saisie

```python
answer = ""
while answer != "oui" and answer != "non":
    answer = input("Continuer ? (oui/non) : ")
print(f"Réponse retenue : {answer}")
```

On répète la question tant que la réponse n'est pas acceptable.
Toujours sans `try` / `except` : validation par conditions et boucles.

---

## Bonnes pratiques (saisie)

- message d'invite explicite (`"Nombre entier : "`, pas juste `"> "`)
- convertir dès que le type numérique est nécessaire
- afficher un feedback (`print`) après une étape importante
- garder les scripts courts et lisibles dans PyCharm

Objectif du jour : un dialogue correct, pas un programme « blindé ».

---

## Conclusion de la séance

- LTI2 se fait dans PyCharm (TI1 : Thonny)
- Projet, Run, console pour la sortie et les erreurs
- `input` lit au clavier et renvoie toujours une `str`
- One-liners : `int(input(...))`, `float(input(...))`, `print(f"...")`
- Casting (`int`, `float`) pour calculer sur la saisie
- Petits menus / dialogues avec conditions et boucles
- Suite : modules (séance 2)

[→ Quiz](quiz_seance_01.html) [→ Exercices](exercices_seance_01.html)
