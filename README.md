
# STM32F446RE — GPIO LED Control

## Description

Ce projet présente une première application de programmation embarquée sur la carte NUCLEO-F446RE.

L'objectif est de configurer et de contrôler la LED utilisateur LD2 à l'aide de la bibliothèque STM32 HAL.

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
- STM32 HAL
- Git et GitHub

## Fonctionnement

Le programme utilise les fonctions suivantes :

- `HAL_GPIO_TogglePin()` : inverse l'état logique de la LED.
- `HAL_Delay()` : introduit une temporisation bloquante.

### Code testé

```c
HAL_GPIO_TogglePin(GPIOA, GPIO_PIN_5);
HAL_Delay(4000);
```

### Résultat obtenu

- LED allumée pendant environ 4 secondes.
- LED éteinte pendant environ 4 secondes.
- Répétition continue du cycle.

La période complète est d'environ 8 secondes.

## Validation expérimentale

L'application a été compilée, programmée et déboguée avec succès sur une carte NUCLEO-F446RE réelle.

Le clignotement de LD2 a été vérifié expérimentalement.

## Perspectives

- Programmation GPIO par accès direct aux registres.
- Étude des registres RCC, MODER, ODR et BSRR.
- Observation des registres avec le débogueur.
- Gestion du bouton utilisateur avec les interruptions EXTI.

## Auteur

**Bilal Bennasser**

- [LinkedIn](https://www.linkedin.com/in/bilalbennasser/)
- [GitHub](https://github.com/bilalbennasser)
