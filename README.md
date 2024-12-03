<p align="left"> <img src="graphique_logo/logo ENSEA.png" width="15%" height="auto" /> </p>

# ESE_2324_AutoRadio

# TP de Synthèse – Autoradio


## 1 Démarrage

 1. On crée un projet pour la carte NUCLEO_L476RG et on initialise les périphériques.
 2. Aprés test, la LED LD2 et l’USART2 connecté à la STLink interne fonctionnent.
 4. On réutilise la fonction printf developpé dans un tp précédent.
 5. On active FreeRTOS en mode CMSIS V1.
 6. On fait fonctionner le shell de trois façon différentes :
(a) Dans une tâche,
(b) En mode interruption,
(c) Avec un driver sous forme de structure.

## 2 Le GPIO Expander et le VU-Metre
### 2.1 Configuration

1. La référence du GPIO Expander est MCP23S17 E/SO. Vous pouvez retrouver sa datasheet dans le dossier datasheet de ce projet github.
2. Sur le STM32, le SPI est utilisé dans notre projet est le SPI 3 
3. Quels sont les paramètres à configurer dans STM32CubeIDE ?
4. Configurez-les.
 
### 2.2 Tests

1. On fait clignoter la LED GPA6.
2. Pour toutes les tester, on va faire preuve d'originalité et faire un chenillard .


### 2.3 Driver

1. Écrivez un driver pour piloter les LED. Utilisez une structure.
2. Écrivez une fonction shell permettant d’allumer ou d’éteindre n’importe
quelle LED.

## 3 Le CODEC Audio SGTL5000
### 3.1 Configuration préalables

Le CODEC a besoin de deux protocoles de communication :

 — L’I2C pour la configuration,
 
 — L’I2S pour le transfert des échantillons audio.
 
Les configurations suivantes sont à faire sur le logiciel STM32CubeIDE dans
la partie graphique CubeMX. Le protocole I2S est géré par le périphérique SAI
(Serial Audio Interface).
1. Quelles pins sont utilisées pour l’I2C ? À quel I2C cela correspond dans le
STM32 ?
2. Activez l’I2C correspondant, laissez la configuration par défaut.
3. Configurez le SAI2 :
   
— SAI A : Master with Master Clock Out,

— Cochez I2S/PCM protocol,

— SAI B : Synchronous Slave,

— Cochez I2S/PCM protocol.

5. Si nécessaire, déplacez les signaux sur les bonnes broches. Vous pouvez
déplacer une broche avec un [Ctrl+Clic Gauche]. Les signaux du SAI
doivent être connectés au broches suivantes :














