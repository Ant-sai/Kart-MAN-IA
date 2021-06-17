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

L'installation de l'environement donkeycar :
Cette installation doit être réalisé sur une raspberry.
 
 1: Flasher votre carte SD avec un nouvel OS Raspbian pour que celle-ci soit comme neuve ;)
 
 2: Vous devez ensuite établire une connexion SSH avec votre PI pour cela vous pouvez y acceder graphiquement dans vos paramètres.
 
 3: Une fois la connexion SSH établi vous pouvez connaitre votre adresse IP avec la commande : ```ping raspberrypi.local ```
 
 4: Maintenant que vous connaissez votre adresse ip vous pouvez installer des logiciels tel que putty ou visual studio code pour établir votre connexion
 
 5: Vous pouvez mettre à jour votre systeme avec ces 2 commandes :  ```sudo apt-get update``` ```sudo apt-get upgrade```
 
 6: (Option) changer le mot de passe dans le menu avec la commande: ``` sudo raspi-config ```
 
 7: nous allons maintenant installer les dépendances lié à l'environnement : ``` sudo apt-get install build-essential python3 python3-dev python3-pip python3-virtualenv python3-numpy python3-picamera python3-pandas python3-rpi.gpio i2c-tools avahi-utils joystick libopenjp2-7-dev libtiff5-dev gfortran libatlas-base-dev libopenblas-dev libhdf5-serial-dev libgeos-dev git ntp``` openCV : ``` sudo apt-get install libilmbase-dev libopenexr-dev libgstreamer1.0-dev libjasper-dev libwebp-dev libatlas-base-dev libavcodec-dev libavformat-dev libswscale-dev libqtgui4 libqt4-test ```
 Nous allons maintenant mettre en place un environement python sur la raspberry pour pouvoir isoler les dépendances: 
 ```python3 -m virtualenv -p python3 env --system-site-packages```
```echo "source env/bin/activate" >> ~/.bashrc```
```source ~/.bashrc ``` ces commandes permettent de lancer l'environnement dès le lancement de la pi.

8: Création du dossier d'installation : ```mkdir projects cd projects```

9: On récupère les fichiers depuis le git donkeycar :  ```git clone https://github.com/autorope/donkeycar
                                                        cd donkeycar
                                                        git checkout master``` et on install les dépendances :
                                                        ```pip install -e .[pi]
pip install numpy --upgrade

curl -sc /tmp/cookie "https://drive.google.com/uc?export=download&id=1DCfoSwlsdX9X4E3pLClE1z0fvw8tFESP" > /dev/null
CODE="$(awk '/_warning_/ {print $NF}' /tmp/cookie)"
curl -Lb /tmp/cookie "https://drive.google.com/uc?export=download&confirm=${CODE}&id=1DCfoSwlsdX9X4E3pLClE1z0fvw8tFESP" -o tensorflow-2.2.0-cp37-cp37m-linux_armv7l.whl
pip install tensorflow-2.2.0-cp37-cp37m-linux_armv7l.whl ``` 

10: vérifiez que l'installation est bien faite avec : ``` python -c "import tensorflow" ```

11: pour installer OpenCV (l'outil de traitement d'image) voici 2 commandes qui peuvent marcher : ```sudo apt install python3-opencv``` ```pip install opencv-python ``` et enfin pour vérifier que OpenCV c'est bien installé : ``` python -c "import cv2"```
Super les installations sont fini !
Maintenant nous allons créer notre application donkeycar.

11: création du dossier ```donkey createcar --path ~/mycar```

12: dans ce fichier vous pourrez modifier quelques propriétés de la voiture :```cd ~/mycar
nano myconfig.py```

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
- Ant-sai: https://github.com/Ant-sai
- Indianat: https://github.com/Indianaat
