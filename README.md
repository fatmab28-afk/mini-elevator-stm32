# mini-elevator-stm32
Projet académique : mini ascenseur conçu avec STM32, keypad 4×3 et LCD. Deux moteurs assurent le mouvement de la cabine et la porte. Développement en C avec HAL, gestion d’étages, sécurité, affichage dynamique et automatisme complet.

## Objectifs techniques
- Authentification sécurisée : activation du système uniquement après saisie correcte du code.  
- Affichage intuitif : instructions pas à pas via l’écran LCD.  
- Commande motorisée : ouverture automatique de la porte (N20), déplacement de la cabine (DC).  
- Réactivité et fiabilité : réponses immédiates aux entrées utilisateur.

## Matériel utilisé
- **Carte STM32F446RE** : ARM Cortex-M4, 180 MHz, 512 Ko Flash, 128 Ko RAM, GPIO, Timers, PWM, UART/SPI/I2C/CAN.  
- **Motoréducteur N20** : commande porte.  
- **Motoréducteur DC** : commande cabine.  
- **Pont H L298N** : pilotage des moteurs DC.  
- **Keypad 4x3** : saisie utilisateur.  
- **LCD 16x2** : affichage dynamique.  
- **Alimentation 12V** : moteur et L298N.  
- **Plaque à essai / Breadboard** : prototypage.

## Fonctionnement
1. L’utilisateur saisit un code sur le keypad (par ex. "000").  
2. La STM32 vérifie le code : si incorrect → message d’erreur, sinon → affichage "Success".  
3. Le moteur de la porte (N20) s’active : ouverture → pause → fermeture.  
4. Le moteur de la cabine (DC) déplace la cabine verticalement vers l’étage sélectionné.  
5. LCD affiche les étapes : “Enter Code”, “Success”, “Cabine en mouvement”, etc.

## Architecture du système
- **Phase d’entrée utilisateur** : lecture keypad et affichage LCD.  
- **Phase de vérification** : contrôle du code saisi.  
- **Phase mécanique** : commande des moteurs (porte + cabine) via PWM et timers.  
- **Interruptions EXTI** : lecture rapide et fiable du clavier.

## Programmation
- **Environnement** : STM32CubeIDE, HAL, langage C.  
- **Périphériques** : GPIO (moteurs et keypad), Timers/PWM (contrôle moteur), LCD 16x2 (mode 4 bits).  
- **Structure** : initialisation → saisie → vérification → commande moteur.  
- **Gestion des interruptions et debounce** pour lecture keypad fiable.

## Schéma des PINs principaux
| Composant | Pins STM32 |
|-----------|------------|
| Keypad    | R1: PB12, R2: PB13, R3: PB14, R4: PB15, C1: PC6, C2: PC7, C3: PC8 |
| Motoréducteur N20 | IN1: PC10, IN2: PC12, ENA: PA6 |
| Motoréducteur DC | IN3: PA8, IN4: PB10, ENB: PA7 |
| LCD 16x2  | EN: PB1, RS: PB2, D4: PB4, D5: PB5, D6: PB6, D7: PB7 |


## Licence
MIT License
