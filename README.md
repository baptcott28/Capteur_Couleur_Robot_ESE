# couleur_fonctionnel
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
