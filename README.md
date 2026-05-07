# 🌌 TP 2 : Lecture Analogique (ADC) - Systèmes Embarqués

Bienvenue dans le dépôt du **Travail Pratique N°2** dédié à l'acquisition de signaux analogiques (ADC) sur le microcontrôleur **STM32 Nucleo-C031C6** en utilisant la bibliothèque HAL (Bare Metal).

Ce projet va bien au-delà de la simple écriture de code C : il s'accompagne d'un **rapport de laboratoire web interactif (HTML/CSS/JS)** intégrant un **Jumeau Numérique (Digital Twin)** pour simuler et visualiser en temps réel la conversion analogique-numérique.

## 🚀 Fonctionnalités du Compte-Rendu Interactif

Le fichier `compte_rendu_tp2.html` est une application web autonome au design "Deep Space" comprenant :
* **Une Page de Garde immersive** avec effet de défilement, respectant les standards académiques.
* **Un Simulateur ADC Dynamique :** Un potentiomètre interactif (slider) qui convertit en temps réel la position physique en une valeur brute ADC (0 - 4095) et en tension correspondante (0.00V - 3.30V). Le simulateur pilote l'état d'une LED virtuelle de manière identique au matériel physique.
* **Le Code Source C intégré** avec coloration syntaxique complète.
* **Une section Post-Lab d'Ingénierie :** Des fiches d'analyse technique détaillées avec formules mathématiques (Résolution 12 bits vs 8 bits, importance du Polling SAR, impact énergétique de l'ADC, résolution du "chattering" via hystérésis, et équation de conversion pour capteur de température LM35).

## 📋 Manipulation Réalisée (Code C & Simulation)

**Lecture d'un Potentiomètre (Mode Polling) :**
* *Code :* Initialisation de l'ADC1 sur la broche `PA0`. Le programme interroge le matériel via `HAL_ADC_Start()`, `HAL_ADC_PollForConversion()`, et `HAL_ADC_GetValue()`. Pour optimiser la consommation énergétique (Low-Power Design), l'ADC est désactivé entre chaque cycle via `HAL_ADC_Stop()`.
* *Logique Matérielle :* Un seuil logiciel est fixé à la moitié de l'échelle 12 bits (valeur numérique : `2048`, soit environ `1.65V`). Si la tension d'entrée dépasse ce seuil, la LED externe sur `PA5` s'allume.

## 🛠️ Matériel & Outils Requis

* **Carte :** STM32 Nucleo-C031C6 (Matériel physique ou simulation virtuelle via [Wokwi](https://wokwi.com/stm32))
* **Composants :** 1x Potentiomètre analogique rotatif, 1x LED, 1x Résistance (220Ω - 330Ω), fils de connexion Dupont.
* **Environnement C :** STM32CubeIDE (Configuration automatique des horloges à 48MHz via CubeMX).
* **Environnement Web :** Navigateur web moderne (Chrome, Firefox, Edge, Safari) pour exécuter le Jumeau Numérique HTML.

## ⚙️ Instructions d'Exécution

### 1. Visualiser le Rapport Interactif (Web)
Double-cliquez sur le fichier `compte_rendu_tp2.html`. Déplacez le curseur du potentiomètre virtuel pour observer la variation simultanée du signal brut (0-4095), de la tension (V), et le déclenchement de la LED au franchissement du seuil VREF/2.

### 2. Simuler le Code C (Wokwi / Matériel)
1. Créez un projet "STM32 Nucleo64 C031C6" (ou utilisez votre carte physique).
2. Câblage :
   * La broche de signal central (SIG) du potentiomètre sur **PA0**.
   * Les broches d'alimentation (VCC et GND) du potentiomètre sur le **3V3** et le **GND** de la carte Nucleo.
   * Une LED (en série avec sa résistance) sur la broche **PA5**.
3. Insérez le code C fourni (fichiers `main.c` et `main.h`) généré pour ce TP.
4. Lancez l'exécution/simulation et ajustez le potentiomètre pour tester la boucle d'acquisition.

## 👥 Équipe du Projet

**Année Universitaire :** 2025/2026
* **Binôme :** Dahane Ahmed Lamine & Tabbi Meriem
* **Enseignante Responsable :** Mme. Afaf Saoud
