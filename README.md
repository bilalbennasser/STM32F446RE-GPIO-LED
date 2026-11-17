# STM32F446RE — GPIO LED Control

## Description
Ce projet présente une première application de programmation embarquée sur la carte NUCLEO-F446RE.

L'objectif est de configurer et contrôler une LED en utilisant la bibliothèque STM32 HAL.

## Matériel
- Carte : NUCLEO-F446RE
- Microcontrôleur : STM32F446RE
- Processeur : ARM Cortex-M4
- LED utilisateur : LD2 (PA5)
- Programmateur : ST-LINK intégré

## Environnement de développement
- Langage : C
- STM32CubeIDE 2.2.0
- STM32CubeMX
- STM32 HAL
- Git et GitHub

## Fonctionnement
La fonction HAL_GPIO_TogglePin() permet d'inverser l'état de la LED LD2.

La fonction HAL_Delay() permet de définir le temps entre deux changements d'état.

Exemple testé :

```c
HAL_GPIO_TogglePin(GPIOA, GPIO_PIN_5);
HAL_Delay(4000);
```

Résultat :
- LED allumée pendant environ 4 secondes
- LED éteinte pendant environ 4 secondes
- Répétition en boucle infinie

## Validation expérimentale
Le programme a été compilé, transféré et exécuté sur une carte NUCLEO-F446RE réelle.

Le fonctionnement de la LED a été vérifié avec succès.

## Perspectives
- Contrôle GPIO par accès direct aux registres
- Étude des registres RCC, MODER et BSRR
- Débogage et observation des registres
- Gestion d'un bouton par interruption EXTI

## Auteur
Bilal Bennasser
