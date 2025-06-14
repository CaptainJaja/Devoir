# Ressources, tutoriels et devoirs d'été

Ce dépôt regroupe toutes les ressources à consulter ainsi que les devoirs à réaliser pendant l'été pour l'équipe **INFO** (et **MECA** quand indiqué). Chaque répertoire **doit obligatoirement contenir un `README.md`** récapitulant son contenu.

---

## 1. Git / GitHub

* **Tuto vidéo (playlist)** : [https://www.youtube.com/watch?v=3RjQznt-8kE\&list=PL4cUxeGkcC9goXbgTDQ0n\_4TBzOO0ocPR\&index=2](https://www.youtube.com/watch?v=3RjQznt-8kE&list=PL4cUxeGkcC9goXbgTDQ0n_4TBzOO0ocPR&index=2)
* **À retenir**

  * Familiarisez‑vous avec Git : clonage, branches, commits, pull‑requests.
  * Chaque répertoire doit contenir un **`README.md`** clair et concis.
    → Si vous n'êtes pas à l'aise avec Markdown, demandez à ChatGPT ; il peut générer la mise en forme pour vous.

---

## 2. PuTTY

* **Prise en main (vidéo)** : [https://www.youtube.com/watch?v=4YVizsRCQcg](https://www.youtube.com/watch?v=4YVizsRCQcg)
* Objectif : savoir utiliser PuTTY comme moniteur série pour dialoguer avec votre carte STM32.

---

## 3. CAO 3D  – Devoir *TEAM MECA* (***TEAM INFO*** bienvenue !)

| Ressource                              | Contenu                                                                                                                                                                       |
| -------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Tuto fonctionnalités                   | [https://www.youtube.com/watch?v=tdRpa7EglGM\&list=PLRhna5\_X7uWv6LsV-2kZWrDOdz\_TsI0UK](https://www.youtube.com/watch?v=tdRpa7EglGM&list=PLRhna5_X7uWv6LsV-2kZWrDOdz_TsI0UK) |
| Tuto projet Onshape (assemblage, etc.) | [https://www.youtube.com/watch?v=GYkZmE\_6MpY](https://www.youtube.com/watch?v=GYkZmE_6MpY)                                                                                   |

> **À faire** : **Exercice 2** du poly *maker* (*Exercice 3* pour les plus motivés 🔥).

---

## 4. STM32 : ressources officielles

* **Wiki principal** : [https://wiki.st.com/stm32mcu/wiki/Main\_Page](https://wiki.st.com/stm32mcu/wiki/Main_Page)

### 4.1 GPIO

* Guide « Getting started » : [https://wiki.st.com/stm32mcu/wiki/Getting\_started\_with\_GPIO](https://wiki.st.com/stm32mcu/wiki/Getting_started_with_GPIO)
* Vidéo d'introduction : [https://www.youtube.com/watch?v=TSDS3op91TE](https://www.youtube.com/watch?v=TSDS3op91TE)
* Savoir :

  * Signification des pin *TTL* / *FT*.
  * Rôle de **`GPIO output level`**.
  * Différences **Push‑Pull vs Open‑Drain**.
  * Usage des *pull‑up* / *pull‑down*.
  * Renommer / *labeller* une pin dans STM32CubeMX.

### 4.2 EXTI (interruptions externes)

* Guide : [https://wiki.st.com/stm32mcu/wiki/Getting\_started\_with\_EXTI](https://wiki.st.com/stm32mcu/wiki/Getting_started_with_EXTI)
* À comprendre : configuration de l'EXTI dans CubeMX et gestion dans le code.

### 4.3 DMA

* Guide : [https://wiki.st.com/stm32mcu/wiki/Getting\_started\_with\_DMA](https://wiki.st.com/stm32mcu/wiki/Getting_started_with_DMA)
* Vidéo explicative : [https://www.youtube.com/watch?v=zipjCtiHYr8\&t=884s](https://www.youtube.com/watch?v=zipjCtiHYr8&t=884s)
* À savoir : principe du DMA, configuration et utilisation pour l'UART, l'ADC, etc.

### 4.4 UART

* Guide : [https://wiki.st.com/stm32mcu/wiki/Getting\_started\_with\_UART](https://wiki.st.com/stm32mcu/wiki/Getting_started_with_UART)
* Mini‑projet (vidéo) : [https://www.youtube.com/watch?v=dEQwSl8mCFs\&t=2s](https://www.youtube.com/watch?v=dEQwSl8mCFs&t=2s)

### 4.5 ADC

* Guide : [https://wiki.st.com/stm32mcu/wiki/Getting\_started\_with\_ADC](https://wiki.st.com/stm32mcu/wiki/Getting_started_with_ADC)
* Mise en pratique : [https://www.youtube.com/watch?v=deMF2xu\_ASQ\&t=108s](https://www.youtube.com/watch?v=deMF2xu_ASQ&t=108s)

---

## 5. FreeRTOS

* Introduction vidéo : [https://www.youtube.com/watch?v=OPrcpbKNSjU](https://www.youtube.com/watch?v=OPrcpbKNSjU)

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
* Shell FreeRTOS+CLI pour entrer les commandes.
* Statistiques CPU (`vTaskGetRunTimeStats`).
* Mode multi‑joueur (classement).
* Bascule en mode basse consommation entre deux parties.

---

## 7. Rappel important

> **Tout répertoire du dépôt doit contenir un `README.md` décrivant son contenu, les pré‑requis et la manière de lancer l'exemple ou d'ouvrir les fichiers.**

---

🏁 **Bon travail à tous et bel été !**
