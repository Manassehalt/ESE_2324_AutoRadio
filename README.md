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

Code : "void MCP23S17_Init(void) {
    uint8_t data[3];

    HAL_GPIO_WritePin(CS_GPIO_PORT, CS_PIN, GPIO_PIN_SET);   // CS HIGH
    HAL_Delay(1);

    data[0] = 0x40; // Adresse du registre IODIRB
    data[1] = 0x01; // Toutes les broches configurées comme sorties
    data[2] = 0x00;
    HAL_Delay(1);
    HAL_GPIO_WritePin(CS_GPIO_PORT, CS_PIN, GPIO_PIN_RESET); // CS LOW
    HAL_Delay(1);
    HAL_SPI_Transmit(&hspi3, data, 3, HAL_MAX_DELAY);
    HAL_Delay(1);
    HAL_GPIO_WritePin(CS_GPIO_PORT, CS_PIN, GPIO_PIN_SET);   // CS HIGH
}

void MCP23S17_WriteGPIOA(uint8_t gpioa_state) {
    uint8_t data[3];

    data[0] = 0x40;
    data[1] = 0x12;
    data[2] = gpioa_state;
    HAL_GPIO_WritePin(CS_GPIO_PORT, CS_PIN, GPIO_PIN_RESET);
    HAL_SPI_Transmit(&hspi3, data, 2, HAL_MAX_DELAY);
    HAL_GPIO_WritePin(CS_GPIO_PORT, CS_PIN, GPIO_PIN_SET);
}
void MCP23S17_WriteGPIOB(uint8_t gpiob_state) {
    uint8_t data[3];

    data[0] = 0x40;
    data[1] = 0x13;
    data[2] = gpiob_state;
    HAL_GPIO_WritePin(CS_GPIO_PORT, CS_PIN, GPIO_PIN_RESET);
    HAL_SPI_Transmit(&hspi3, data, 3, HAL_MAX_DELAY);
    HAL_GPIO_WritePin(CS_GPIO_PORT, CS_PIN, GPIO_PIN_SET);
}
void Blink_LED(void) {
    printf("ENTERED FUNCTION\r\n");

    MCP23S17_WriteGPIOB(0xFF);
    printf("GPIOB LEDs ON\r\n");

    HAL_Delay(1000);
    printf("TEST DELAY\r\n");

    MCP23S17_WriteGPIOB(0x00);
}

"


3. Pour toutes les tester, on va faire preuve d'originalité et faire un chenillard .
"void MCP23S17_Chenillard(void) {
    uint8_t chenillard_state = 0x01;
    for (int i = 0; i < 8; i++) {
        MCP23S17_WriteGPIOB(~chenillard_state);
        HAL_Delay(200);
        chenillard_state <<= 1;
    }
}"

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














