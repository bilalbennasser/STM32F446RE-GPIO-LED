
# STM32F446RE — GPIO LED Control

## Description

Ce projet présente une application de programmation embarquée sur la carte NUCLEO-F446RE.

L'objectif est de contrôler la LED utilisateur LD2 (PA5) en utilisant deux approches :

1. La bibliothèque STM32 HAL.
2. L'accès direct aux registres matériels du microcontrôleur.

Les deux approches ont été testées sur une carte réelle.

## Matériel utilisé

- Carte : NUCLEO-F446RE
- Microcontrôleur : STM32F446RE
- Processeur : ARM Cortex-M4
- LED utilisateur : LD2 (PA5)
- Programmateur / Débogueur : ST-LINK intégré

## Environnement de développement

- Langage : Embedded C
- STM32CubeIDE 2.2.0
- STM32CubeMX
- STM32 HAL et CMSIS
- Git et GitHub

## 1. Contrôle GPIO avec HAL

La première version utilise les fonctions HAL pour contrôler la LED.

```c
HAL_GPIO_TogglePin(GPIOA, GPIO_PIN_5);
HAL_Delay(4000);
```

La fonction `HAL_GPIO_TogglePin()` inverse l'état logique de PA5.

La fonction `HAL_Delay(4000)` introduit une temporisation bloquante d'environ 4 secondes.

Cette version est conservée dans l'historique Git du projet.

## 2. Contrôle GPIO par registres

La version actuelle configure directement PA5 à l'aide des registres du STM32F446RE.

### Configuration de PA5

```c
// Activer l'horloge GPIOA
RCC->AHB1ENR |= RCC_AHB1ENR_GPIOAEN;
(void)RCC->AHB1ENR;

// Etat initial LOW
GPIOA->BSRR = (1U << 21);

// Mode Push-Pull
GPIOA->OTYPER &= ~(1U << 5);

// Low Speed
GPIOA->OSPEEDR &= ~(3U << 10);

// No Pull-up / No Pull-down
GPIOA->PUPDR &= ~(3U << 10);

// PA5 en sortie
GPIOA->MODER &= ~(3U << 10);
GPIOA->MODER |=  (1U << 10);
```

### Boucle principale

```c
while (1)
{
    // LED ON
    GPIOA->BSRR = (1U << 5);
    HAL_Delay(4000);

    // LED OFF
    GPIOA->BSRR = (1U << 21);
    HAL_Delay(4000);
}
```

Le registre BSRR permet de mettre PA5 à l'état haut ou bas.

La temporisation utilise toujours la bibliothèque HAL.

## 3. Registres étudiés

| Registre | Fonction |
|---|---|
| RCC_AHB1ENR | Activation de l'horloge GPIOA |
| GPIOA_MODER | Configuration de PA5 en sortie |
| GPIOA_OTYPER | Configuration Push-Pull |
| GPIOA_OSPEEDR | Vitesse de sortie |
| GPIOA_PUPDR | Configuration Pull-up/Pull-down |
| GPIOA_BSRR | Mise à 1 et remise à 0 de PA5 |
| GPIOA_ODR | Observation de l'état de sortie |

## 4. Validation expérimentale

Les deux versions ont été compilées et testées avec succès sur la carte NUCLEO-F446RE.

Résultats observés :

- LED allumée pendant environ 4 secondes.
- LED éteinte pendant environ 4 secondes.
- Période complète d'environ 8 secondes.
- Fonctionnement validé après suppression de l'initialisation HAL/BSP spécifique à LD2.

Le débogueur de STM32CubeIDE a été utilisé pour examiner les registres GPIO et suivre les modifications lors de l'exécution du programme avec Step Over.

La broche PA5 est configurée directement par registres dans la version finale.

Le projet conserve HAL pour les temporisations et certaines initialisations système et périphériques.

## 5. Perspectives

- Lecture du bouton utilisateur B1 (PC13).
- Comparaison entre Polling et Interruptions.
- Configuration des interruptions EXTI/NVIC.
- Utilisation des Timers pour les temporisations.

## Auteur

**Bilal Bennasser**

- [LinkedIn](https://www.linkedin.com/in/bilalbennasser/)
- [GitHub](https://github.com/bilalbennasser)
