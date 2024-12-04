# ESE_2324_AutoRadio

# TP de Synthèse – Autoradio

## 1 Démarrage
### 1. Créez un projet pour la carte NUCLEO_L476RG. Initialisez les périphériques
avec leur mode par défaut, mais n’activez pas la BSP.
 2. Testez la LED LD2.
 3. Testez l’USART2 connecté à la STLink interne.
 4. Débrouillez-vous pour que la fonction printf fonctionne.
 5. Activez FreeRTOS en mode CMSIS V1.
 6. Faites fonctionner le shell :
(a) Dans une tâche,
(b) En mode interruption,
(c) Avec un driver sous forme de structure.
## 2 Le GPIO Expander et le VU-Metre
### 2.1 Configuration
1. Quelle est la référence du GPIO Expander ? Vous aurez besoin de sa datasheet, téléchargez-la.
2. Sur le STM32, quel SPI est utilisé ?
3. Quels sont les paramètres à configurer dans STM32CubeIDE ?
4. Configurez-les.
### 2.2 Tests
1. Faites clignoter une ou plusieurs LED.
2. Pour toutes les tester, vous pouvez faire un chenillard (par exemple).
ENSEA Page 1/6 TP de Synthèse – Autoradio
### 2.3 Driver
1. Écrivez un driver pour piloter les LED. Utilisez une structure.
2. Écrivez une fonction shell permettant d’allumer ou d’éteindre n’importe
quelle LED.
















