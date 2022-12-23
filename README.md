# couleur_fonctionnel
- calibration fonctionne
- mesure fonctionne
- introduction d'une valeur min de frequence dans h_color_sensor_t et prise en compte dans la mesure
- fonctionne avec freeRTOS actif et demarrage du schedduler
- integration d'une structure de calib au sein d'un sensor
- taches colormeasureTask écrite
- ecriture de fonction de process pour debloquer les semaphore et les donner aux autres taches. Fonctionne avec une tache temoin et la tache coloMeasure dans le main
- on ramene la tache color_measure dans le fichier color_sensor (en cours)

## ne pas oublier 
- set photodiode verte dans l'interruption du bouton
- mettre la fonction sensorHandleCalib avant toutes les autres sinon ca plante jsp pk
