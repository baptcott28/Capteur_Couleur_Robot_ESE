# couleur_fonctionnel
- calibration fonctionne
- mesure fonctionne
- introduction d'une valeur min de frequence dans h_color_sensor_t et prise en compte dans la mesure
- fonctionne avec freeRTOS actif et demarrage du schedduler
- integration d'une structure de calib au sein d'un sensor
- taches colormeasureTask écrite
- reste bloqué dans la tache de mesrure sans toutefois l'executer 
- ecriture de fonction de process pour debloquer la situation précedente -> à voir parce que le rythme de give des semaphore n'est pas bon. Regler ca avant les autres trucs our avoir une fonction de processe qui fonctionne. 

## ne pas oublier 
- set photodiode verte dans l'interruption du bouton
- mettre la fonction sensorHandleCalib avant toutes les autres sinon ca plante jsp pk
