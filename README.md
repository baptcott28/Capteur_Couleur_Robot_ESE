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
- colorMeasureTask s'execute parfaitement sans tâche autour
- test avec les vTaskSuspend(process) (a faire mais modif avec flag de retour de fin de mesure a faire) pour pouvoir mettre des taches autour

## ne pas oublier 
- set photodiode verte dans l'interruption du bouton
- mettre la fonction sensorHandleCalib avant toutes les autres sinon ca plante jsp pk
