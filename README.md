# Kart-MANI-IA

Bienvenue sur le README de l'équipe Kart Man'IA.

Il s’agit d’un projet de construction de voiture autonome au format 1/16ème.

## Pour commencer

Ci-dessous vous trouverez une explication de comment utiliser notre modèle de voiture autonome.

### Matériels

Le matériel requis pour ce projet:

- 1 Raspberry pi 4 
-	1 kit de voiture de Racing (ici le modèle PiRacer Pro de Waveshare)
-	1 circuit avec les caractéristiques suivantes:
  - Largeur: environ 50cm
  - Longueur: comme vous le souhaitez
  - Sol: foncé
  - Bord du circuit: au scotch blanc, bord intérieur: 1 bande, bord extérieur: 2 bandes

### Installation

Les étapes pour configurer la voiture

... à venir ...


## Démarrage
Comment lancer les différents modèles pour lancer la voiture ?

Tout d'abord il faut réaliser un modèle h5 ou tfile. 

###### Entrainement de la voiture

- Placer la voiture sur le circuit
- Lancer la commande suivante qui permet d'enregistrer les données de la caméra et de lancer la voiture:
``` python manage.py drive --js ```
- Prendre la manette et faire tourner la voiture sur le circuit en faisant les meilleures trajectoires possibles
- Faite une ctrl + c pour couper l'enregistrement

###### Réalisation du modèle

- Récupérer les données du dossier ./data sur votre ordinateur personnelle
- Sur anaconda ou mini anaconda, dans le dossier mycar, lancer la commande:
  - Pour un model h5:
``` donkey train --tub ./data --model ./mypilot.h5 --framework tensorflow ```
  - Pour un model tfile:
``` donkey train --tub ./data --model ./mypilot.tflite --framework tensorflow --type tflite_linear ```
A la fin des réalisations des époques vous devriez avoir un fichier h5 ou tfile dans le dossier model
- Mettre le fichier obtenu sur la raspberry dans le dossier mycar/models

###### Lancement de la voiture

- Lancer le modèle avec la commande suivante:
  - Pour un model h5
``` python manage.py drive --model ./models/mypilot.h5 ```
  - Pour un model tfile
``` python manage.py drive --model models/mypilot.tflite --type tflite_linear ```

Votre voiture roule toute seule BRAVO !!!


## Fabriqué avec

Voici les logiciels utilisés pour réaliser ce projet:

- Visual Studio Code
- Putty
- FileZilla

## Versions

Donkeycar : 4.3.0

## Auteurs

Si vous avez des questions vous pouvez contacter:
- Ant-sai: https://github.com/Ant-sai/Kart-MANI-IA.git/Ant-sai
- Indianat: https://github.com/Ant-sai/Kart-MANI-IA.git/contributors
