# Ressources, tutoriels et devoirs d'été

Ce dépôt regroupe toutes les ressources à consulter ainsi que les devoirs à réaliser pendant l'été pour l'équipe **INFO** et **MECA**. Chaque répertoire **doit obligatoirement contenir un `README.md`** récapitulant son contenu.

---

## 1. Git / GitHub

* **Tuto vidéo** : [Playlist YouTube](https://www.youtube.com/watch?v=3RjQznt-8kE&list=PL4cUxeGkcC9goXbgTDQ0n_4TBzOO0ocPR&index=2)
* **À retenir**

  * Familiarisez‑vous avec Git : clonage, branches, commits, pull‑requests.
  * Chaque répertoire doit contenir un **`README.md`** clair et concis.
    → Si vous n'êtes pas à l'aise avec Markdown, demandez à ChatGPT ; il peut générer la mise en forme pour vous.
    → Chaque commit doit avoir un message : -m  "clair indiquant le principal du changement !"

---

## 2. PuTTY

* **Prise en main ** : [Video](https://www.youtube.com/watch?v=4YVizsRCQcg)
* Objectif : savoir utiliser PuTTY comme moniteur série pour dialoguer avec votre carte STM32.

---

## 3. CAO 3D  – Devoir *TEAM MECA* (***TEAM INFO*** bienvenue !)

| Ressource                              | Contenu                                                                                                                                                                       |
| -------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Tuto fonctionnalités                   | [Playlist YouTube](https://www.youtube.com/watch?v=tdRpa7EglGM&list=PLRhna5_X7uWv6LsV-2kZWrDOdz_TsI0UK) |
| Tuto projet Onshape (assemblage, etc.) | [Video YouTube](https://www.youtube.com/watch?v=GYkZmE_6MpY)                                                                                   |

> **À faire** : **Exercice 2** du poly *maker* (*Exercice 3* pour les plus motivés 🔥).

---

## 4. STM32 : ressources officielles

* **Wiki principal** : [ST_Official](https://wiki.st.com/stm32mcu/wiki/Main_Page)

### 4.1 GPIO

* Guide  : [« Getting started »](https://wiki.st.com/stm32mcu/wiki/Getting_started_with_GPIO)
* Vidéo d'introduction : [Video avec plus de détails](https://www.youtube.com/watch?v=TSDS3op91TE)
* Savoir :

  * Signification des pin *TTL* / *FT*.
  * Rôle de **`GPIO output level`**.
  * Différences **Push‑Pull vs Open‑Drain**.
  * Usage des *pull‑up* / *pull‑down*.
  * Renommer / *labeller* une pin dans STM32CubeMX.

### 4.2 EXTI (interruptions externes)

* Guide : [Page_wiki_ST](https://wiki.st.com/stm32mcu/wiki/Getting_started_with_EXTI)
* À comprendre : configuration de l'EXTI dans CubeMX et gestion dans le code.

### 4.3 DMA

* Guide : [Page_wiki_ST](https://wiki.st.com/stm32mcu/wiki/Getting_started_with_DMA)
* Vidéo explicative : [Video YouTube](https://www.youtube.com/watch?v=zipjCtiHYr8&t=884s)
* À savoir : principe du DMA, configuration et utilisation pour l'UART, l'ADC, etc.

### 4.4 UART

* Guide : [Page_wiki_ST](https://wiki.st.com/stm32mcu/wiki/Getting_started_with_UART)
* Mini‑projet  : [Video YouTube](https://www.youtube.com/watch?v=dEQwSl8mCFs&t=2s)

### 4.5 ADC

* Guide : [Page_wiki_ST](https://wiki.st.com/stm32mcu/wiki/Getting_started_with_ADC)
* Mise en pratique : [Video YouTube](https://www.youtube.com/watch?v=deMF2xu_ASQ&t=108s)

---

## 5. FreeRTOS

* Introduction vidéo : [Video YouTube](https://www.youtube.com/watch?v=OPrcpbKNSjU)

### Questions à maîtriser après visionnage

1. **Qu'est‑ce que FreeRTOS ?**
2. **Qu'est‑ce que le SysTick ?**
   Pourquoi l'intervenant préfère‑t‑il utiliser **TIM6** comme source de *time‑base* ?
3. **Que fait `osDelay()` ?**
   Quelle différence avec `HAL_Delay()` ?
4. **Que fait l'appel `osKernelStart();` dans `main()` ?**
   Peut‑on appeler `printf()` dans le `while(1)` qui suit ? Pourquoi ?
5. **Que fait `osThreadTerminate(NULL)` ?**
6. **En quoi FreeRTOS est‑il utile dans nos projets ?**

---

## 6. Devoir *TEAM INFO*  – Jeu LED sous FreeRTOS (***TEAM MECA*** bienvenue !)

**Principe général** : réaliser un mini‑jeu de réflexe entièrement piloté via **PuTTY** (moniteur série). Le code tourne sur une carte **STM32** (ex. NUCLEO‑L476RG) avec **FreeRTOS**.

### 6.1 Règles du jeu

1. **Attente joueur** – LED éteinte :

   ```text
   En attente du joueur (appuyez pour commencer le match)
   ```
2. **Premier appui / commande** – démarrage :

   ```text
   Bouton appuyé ! Le jeu commence  ||  Score : 0 pts
   ```
3. **Phase de jeu (1 minute)**

   * La LED s'allume pendant **200 ms**, de façon aléatoire toutes les 5 s (±) ;
   * Le joueur dispose de **500 ms** pour appuyer.
4. **Détection de triche** (appui avant l'allumage) :

   ```text
   Triche détectée. Pénalité : Score -1  ||  Score : X pts
   ```
5. **Appui trop tardif** (>500 ms) :

   ```text
   Pas assez rapide, score inchangé  ||  Score : X pts
   ```
6. **Succès** (<500 ms) :

   ```text
   Bien joué ! Score +1  ||  Score : X pts
   ```
7. **Fin de partie** (après 60 s) :

   ```text
   Fin du jeu, voici votre score : X pts
   ```

### 6.2 Contraintes techniques minimales

* **Affichage uniquement via PuTTY** – aucun `printf()` dans CubeIDE.
* Utilisation de **FreeRTOS** : au moins 3 tâches (LED, Bouton, Jeu) + timers.
* Anti‑rebond logiciel (<20 ms) sans blocage *busy‑wait*.
* Horloge : `configTICK_RATE_HZ = 1000` (résolution 1 ms).
* Communication série non bloquante (DMA recommandé).
* Robustesse : aucune *HardFault*, retour au menu d'attente après chaque partie.

### 6.3 Extensions possibles (bonus)

* Table de scores persistante en Flash.
* Mode multi‑joueur (classement).
* Bascule en mode basse consommation entre deux parties.

---

## 7. Rappel important

> **Tout répertoire du dépôt doit contenir un `README.md` décrivant son contenu, les pré‑requis et la manière de lancer l'exemple ou d'ouvrir les fichiers.**

---



# Guide de style C pour un code propre et lisible

## 1. Nommage : la première clé de lisibilité

| Élément                                 | Convention courante          | Exemples 📝                                             | Notes                                        |
| --------------------------------------- | ---------------------------- | ------------------------------------------------------- | -------------------------------------------- |
| **Constantes & macros**                 | `UPPER_SNAKE_CASE`           | `SIZE_MAX`, `BUFFER_LEN`                                | Préfixe de module si global : `CFG_MAX_SIZE` |
| **Types (`struct`, `enum`, `typedef`)** | `PascalCase`                 | `typedef struct Node Node;`, `enum Color { Color_Red }` | Évite le suffixe `_t` (réservé par POSIX).   |
| **Fonctions**                           | `snake_case` ou `PascalCase` | `read_config()`, `ListInit()`                           | Choisir un style et s’y tenir.               |
| **Variables locales**                   | `lower_snake_case`           | `line_count`, `tmp_buf`                                 | Pas d’abréviations cryptiques.               |
| **Membres de struct**                   | `lower_snake_case`           | `height`, `next`                                        | Même règle que les variables.                |
| **Valeurs d’énumération**               | `Prefix_ENUM_VALUE`          | `Color_Red`, `State_Error`                              | Préfixe pour éviter les collisions.          |

---

## 2. Formatage et indentation

```c
/* 4 espaces ; style K&R recommandé */
if (cond) {
    do_something();
} else {
    handle_error();
}
```

* **Indentation** : 4 espaces (ou TAB partout, mais jamais les deux).
* **Longueur de ligne** : 80 – 100 caractères max.
* **Espaces** :

  * après chaque virgule ;
  * avant l’astérisque des pointeurs dans les déclarations (`char *ptr`) ;
  * autour des opérateurs.
* Pas d’espace après `(` ni avant `)`.

---

## 3. Organisation des fichiers

1. **Un module = un duo `file.h` / `file.c`.**
2. Ordre des `#include` :

   1. Standard C (`<stdio.h>`, `<stdlib.h>`…)
   2. Bibliothèques tierces (`<third_party/foo.h>`)
   3. Headers du projet (`"project_local.h"`)
      (séparés par une ligne vide)
3. Protéger chaque header :

```c
#ifndef PROJECT_MODULE_H
#define PROJECT_MODULE_H
/* … */
#endif /* PROJECT_MODULE_H */
```

Ou `#pragma once` si le compilateur le gère.

---

## 4. Commentaires & documentation

* Explique **pourquoi** (le contexte), pas **quoi** (le code le montre déjà).
* Format **Doxygen** apprécié :

```c
/**
 * @brief Initialise la liste chaînée.
 * @return 0 en cas de succès, -1 sinon.
 */
int list_init(List *list);
```

---

## 5. Fonctions : clarté et responsabilité unique

| Bonne pratique                            | Raison                               |
| ----------------------------------------- | ------------------------------------ |
| Prototype dans le `.h`, code dans le `.c` | Sépare interface/détail.             |
| **Responsabilité unique**                 | Plus simple à tester et à maintenir. |
| ≤ 5 paramètres                            | Lisibilité et refactorisation.       |
| Retour explicite du statut                | `0` = OK, `<0` = erreur.             |

---

## 6. Constantes, macros, `enum` et `static const`

```c
static const double PI = 3.141592653589793;
enum { MAX_RETRY = 3 };
#define SQR(x) ((x) * (x))   /* parenthèses ! */
```

* **Préférer** `static const` ou `enum` (typés) aux macros pour de simples valeurs.
* Les macros (`#define`) : uniquement pour le préprocesseur (options de compilation, méta-programming).

---

## 7. Gestion de la mémoire & des ressources

1. **Chaque `malloc` a son `free`** (idéalement dans le même module).
2. Modèle *acquire-init-use-release* (pattern `goto fail` pour la sortie propre).
3. Helper : `safe_malloc()`, macros `BUF_FREE(ptr)`…

---

## 8. Sécurité et robustesse

* Compiler avec tous les warnings :

  ```bash
  -Wall -Wextra -Wpedantic
  ```

  (`-Werror` en CI pour refuser les warnings)
* Types fixes : `stdint.h` (`uint32_t`, `int64_t`…).
* Toujours vérifier les valeurs de retour des I/O (`fread`, `write`, `printf`…).
* Initialiser toutes les variables.

---

## 9. Tests & CI

* Unit-tests : **Unity**, **Ceedling**, **CMock**, **CTest**…
* CI automatique : build + tests + analyse statique (`clang-tidy`, `cppcheck`, Coverity) + formatteur (`clang-format`).

---

## 10. Cohérence avant tout !

> Rédige un fichier **`CODING_STYLE.md`**, choisis tes règles, applique-les **partout**.
> Code homogène = relectures plus rapides, maintenance plus facile, développeurs plus heureux !

---

### Référence express

```text
• MACROS_ET_CONSTANTES    UPPER_SNAKE_CASE
• types (struct, enum)    PascalCase
• fonctions               snake_case
• variables & champs      lower_snake_case
• 4 espaces, K&R braces, 80–100 colonnes
• headers : <stdio.h> puis <lib.h> puis "local.h"
• #ifndef FOO_H / #define FOO_H / #endif
• -Wall -Wextra -Wpedantic
• chaque malloc → free ; vérifier retours
```




🏁 **Bonne écriture de code, bon travail à tous et bel été !**
