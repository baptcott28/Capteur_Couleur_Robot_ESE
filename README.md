# Capteur couleur 

Ce projet a pour but de produire un code opérable en vue d'utiliser le capteur de couleur de chez DFRobots basé sur le capteur RGB TCS3200. 

Ce capteur renvoie une fréquence en fonction de la couleur observée. Il est constitué de 4 filtres, chacun sensibles à une couleur précise. 

![image](https://github.com/baptcott28/couleur_fonctionnel/blob/main/capteur%20couleur.jpg)

Datasheet disponible [ici](https://wiki.dfrobot.com/TCS3200_Color_Sensor__SKU_SEN0101_).


## Détection d'une couleur

La stratégie de détection d'une couleur est simple. Il suffit de réaliser une mesure de la fréquence renvoyée par le capteur pour chaque filtre disponible. La couleur observée correspond à la couleur du filtre pour laquelle la fréquence renvoyée est la plus élevée.

## Création structure du capteur

Pour pouvoir utiliser le capteur, il faut d'abord créer une structure, ce qui va faciliter l'intéraction de l'utilisateur avec ses paramètres.

```C
typedef struct h_color_sensor_t{
	...
}h_color_sensor_t;
``` 

Dans cette structure (définie dans `color_sensor.h`), il y a trois sous-structures qui sont nécessaires pour la calibration du capteur. Une qui va servir à stocker l'avancée de la calibration, tandis que les deux autres vont stocker des données relatives aux résultats de cette calibration.

## Fonctions spéciales 

```C
void colorSensorHandleInputCapture_IT(h_color_sensor_t * h_color_sensor,TIM_TypeDef *TIM)
``` 
Cette fonction est à mettre dans l'interruption en INPUT_CAPTURE liée au retour de la fréquence du capteur. 

## Initialisation du capteur

Il y a plusieurs valeur de paramétrage du capteur, à choisir dans la datasheet. 

Les fonctions suivantes sont des fonctions d'initialisation : 
 ```C 
- void colorSensorInit(h_color_sensor_t * h_color_sensor, color_sensor_color_t color, color_sensor_output_scale_t output_scale, color_sensor_state_t state);
``` 
Avec `output_scale` une macro définie, `state` l'état du capteur (enable/disable), `color` la couleur du filtre appliqué à la fin de l'initialisation, `h_color_sensor` la structure du capteur précédement créée. 

## Calibration

La calibration est un processus essentiel de l'utilisation du capteur qui est à faire à chaque mise sous tension. Il y a 4 états : 
```C
typedef enum calibration_state_enum{
	WAINTING_FOR_CALIB=0,
	CALIB_VERT_CANETTE=1,
	CALIB_VERT_VIDE=2,
	CALIB_ROUGE_CANETTE=3,
	CALIB_ROUGE_VIDE=4,
	CALIB_DONE=5
}calibration_state_t;
``` 
Cette calibration est à réaliser avec une console ouverte et un lien physique entre le PC et la structure opérant le capteur.  

Lancer la fonction `color_sensor_init()`, qui va initialiser le capteur. lancer ensuite la fonction `colorHandleCalibrationSensor()` se laisser ensuite guider par les indications de la console. Idéalement, il faut pointer le capteur vers une source lointaine, sans couleur directement observable, lors des états "VIDES". Le but du jeu est d'avoir le plus grand écart entre deux valeurs de calibration. 

Ces deux valeurs serviront à constituer la transformation affine necessaires a la conparaison des couleurs.

## freeRTOS

Ce projet est compatible freeRTOS. Il y a donc toutes les fonctions pour crer les taches relatives à l'operabilité du capteur. 




## Test avancement librairie
- calibration fonctionne
- mesure fonctionne
- introduction d'une valeur min de frequence dans h_color_sensor_t et prise en compte dans la mesure
- fonctionne avec freeRTOS actif et demarrage du schedduler
- integration d'une structure de calib au sein d'un sensor
- taches colormeasureTask écrite
- ecriture de fonction de process pour debloquer les semaphore et les donner aux autres taches
- Fonctionne avec une tache temoin et la tache colorMeasure (affichage uniquement) dans color_sensor.c et la fonction de calib au debut
- test avec un declenchement de mesure dans colormeasureTask 
- fonctionne avec une distance inferieure au cm VS la surface a mesurer
- colorMeasureTask s'execute parfaitement declenchée par l'obtention de son sémaphore tandis que tache bidon attend son sémaphore qui n'arrivera jamais parce que le robot est dans l'état mesure   

## ne pas oublier 
- set photodiode verte dans l'interruption du bouton
- mettre la fonction sensorHandleCalib avant toutes les autres sinon ca plante jsp pk
