# PROJECT_MTSC_NODE_RED

Bienvenue dans notre solution de détection d'intrusion. Notre projet offre une réponse aux défis de surveillance en combinant l'intelligence des réseaux de caméras avec la flexibilité de Node-Red.

# AUTEURS - ETUDIANT M2 CNS SOUS PARCOURS SR

<ul>
  <li>CISSE Hamadoun</li>
  <li>LAIB Ramy</li>
  <li>SARAOUI Keltouma</li>
  <li>IWOBA REBET Emmanuel</li>
</ul>

# ENCADREUR

MASSINISSA Hamidi

# Principales fonctionnalités

<b>Détection d'Intrusion Intelligente :</b> Grâce au modèle de <b>détection d'object (coco-ssd)</b>, notre système identifie de manière fiable les intrusions, garantissant une réaction proactive à toute menace potentielle.

<b>Notification Instantanée :</b> L'utilisateur est informé en temps réel dès qu'une activité suspecte est détectée, garantissant une réponse rapide et efficace. On utilise <b>Telegram</b> pour l'envoie des notifications et des capture vidéos.


<b>Visualisation en Direct :</b> Le système permet un accès immédiat à la sortie de la caméra concernée, offrant une compréhension visuelle précise de la situation en cours. La sortie de la caméra est streamée en direct sur une page web accéssible de partout.

<b>Optimisation de trafic : </b> Notre système est concu de telle sorte à optimiser les trafics sur le réseau en réduisant au maximum les répétitions d'alertes liés à une meme intrusion. On a mis en place un filtre permettant de filter le trafic rédondant.

# Fonctionnement :

Le fonctionnement du système est décrit comme suit :
<ol type="1">
<li>On démarre le système</li>
<li>Pour chaque camera</li>
          <ol type='i'>
            <li>On capture une frame</li>
            <li>On passe le frame au modèle de détection d'objection</li>
            <li>Si la sortie du modèle est une personne alors </li>
                      <ol type='a'>
                          <li>Si c'est une détection avant rien alors </li>
                              <ul>
                              <li>On notifie l'utilisateur</li>
                              <li>On fait une capture vidéo de 30 sécondes que on envoie à l'utilisateur</li>
                              <li>On retourne à i</li>
                              </ul>
                          <li>Si c'est une détection alors qu'une capture est en cours alors</li>
                              <ul>
                              <li>On notifie pas l'utilisateur</li>
                              </ul>  
                      </ol>
            <li>On retourne à i </li>
          </ol>
</ol>

# Prérequis

<ul>
  <li>Système d'exploition : Linux (Dans notre cas Lubuntu)</li>
  <li>Disposer de docker installer sur votre machine. Si ne l'avez voilà pas, voilà un <a href="https://www.digitalocean.com/community/tutorials/how-to-install-and-use-docker-on-ubuntu-20-04-fr">lien</a> vers un tutoriel très facile pour l'installer.</li>
  <li>Disposer d'un réseau connecté à internet (Indispensable pour pouvoir envoyer les notifications via l'api Telegram)</li>
  <li>Disposer deux camera IP au moins. Dans notre cas, nous avons simuler nos smartphones comme camera à l'aide de l'application <a href="https://play.google.com/store/apps/details?id=com.pas.webcam&hl=fr&gl=US">IP Webcam</a> disponible sur playstore et Applestore.</li>
  <li>Créer un Bot telegram pour pouvoir l'intégrer au système pour les notifications. Voici un lien vers une <a href="https://www.youtube.com/watch?v=rOopUOmsdW8">vidéo</a> pour en créer un.</li>
  <li>Installer Git pour pouvoir cloner le dépot actuel de ce projet et installer le projet.</li>
</ul>


# Comment Commencer :

Après avoir effectué tous les prérequis ci dessus, il faut passer aux étapes suivantes :
<ul>
<li>Installation de Node Red : Notre image docker est basé sur l'image <a href="https://hub.docker.com/layers/nodered/node-red/3.1.0-debian/images/sha256-58529234bb6dc77cf443f92eda90ff268ee84f9268b26da2fd383d5607d2d5c7?context=explore">nodered/node-red:3.1.0-debian</a> qu'on a customisé pour ajouter la bibliothèque <b>FFmpeg</b> pour capturer et manipuler les flux vidéos en stréaming. Pour l'installation du container, on fait :
  <br>
 Cloner le dépôt actuel
  
`` git clone https://github.com/hamadouncisse/PROJECT_MTSC_NODE_RED.git ``

Aller dans le répertoire node_red

`` cd PROJECT_MTSC_NODE_RED/node_red ``

Construiser l'image docker

``  docker image build -t "test_red_node" .  ``

Lancer le conteneur docker

`` docker run -p 1880:1880 -v node_red_data:/data test_red_node ``

Ensuite il suffit d'ouvrir le navigateur et d'aller depuis votre naviguateur web sur le lien http://127.0.0.1:1880/ pour démarrer node.
 
</li>
<li> Installation des bibliothèques de Node Red : Pour que le système fonctionne correctement, il est indispensable d'installer certaines bibliothèques. Dans le menu node red, il faut aller dans l'onglet manage palette, chercher et installer les bibliothèques suivantes :


![image](https://github.com/hamadouncisse/PROJECT_MTSC_NODE_RED/assets/104743493/3f8a5d6a-6f4f-4214-8898-4aef66c2c710 "manage palette 1")

![image1](https://github.com/hamadouncisse/PROJECT_MTSC_NODE_RED/assets/104743493/e0970096-a57d-4773-b7ff-a4232742560c "manage palette 2")

Les bibliothèques sont : 
<ol type="1">
  <li>node-red-contrib-browser-utils</li>
  
  <li>node-red-contrib-image-tools</li>
  
  <li>node-red-contrib-tf-function</li>
  
  <li>node-red-contrib-tf-model</li>
  
  <li>node-red-contrib-tfjs-coco-ssd</li>
  
  <li>node-red-contrib-telegrambot</li>
  
  <li>node-red-contrib-image-output</li>
  
  <li>node-red-node-rbe</li>
  
</ol>

</li>

<li>Importation du flow dans Node Red : Il suffit de selectionner l'onglet <b>Import</b> dans le menu de node red. Ensuite il faut sélectionner le fichier json à importer depuis l'explorateur de fichier.
  
![Alt text](https://nodered.org/docs/user-guide/editor/images/editor-import.png "menu import")

<b style="text-center">Une visulation du flow importé est donnée par la capture suivante :</b>

![Alt text](https://github.com/hamadouncisse/PROJECT_MTSC_NODE_RED/blob/main/all.png "menu import")

</li>
<li>
Configuration des adresses IP des cameras : Dans notre cas, il existe plusieurs noeuds ou l'adresse IP de la caméra est spécifier pour capturer le flux vidéo. Pour l'adapter au votre, il faut remplacer les adresses présentes par les votres dans le noeud suivant :
  
<ol type="1">
  <li>Decode RTSP stream 2</li>
  
  <li>function</li>
  
  <li>notification</li>
  
  <li>notification2</li>
  
  <li>Capture video</li>
</ol>


| Decode RTSP stream                            | Notification                            |
| ----------------------------------- | ----------------------------------- |
| ![Decode RTSP stream](https://github.com/hamadouncisse/PROJECT_MTSC_NODE_RED/blob/main/exec.png) | ![notification](https://github.com/hamadouncisse/PROJECT_MTSC_NODE_RED/blob/main/save1.png) |

Dans le Decode RTSP Stream on a cette commande :

`` ffmpeg -i http://192.168.43.164:8080/video -r 10 -t 30 -y -c:v libx264 -c:a copy /data/video2.mp4 ``


<b>- ffmpeg:</b> Le nom du programme que vous exécutez, qui est FFmpeg dans ce cas.

<b>-i http://192.168.43.164:8080/video:</b> Spécifie l'URL du flux vidéo en tant qu'entrée pour la commande.

<b>-r 10:</b>  Définit le taux de trame (frame rate) de la vidéo de sortie à 10 images par seconde.

<b>-t 30:</b>  Limite la durée de la vidéo de sortie à 30 secondes.

<b>-y:</b>  Force l'écrasement du fichier de sortie s'il existe déjà, sans demander de confirmation.

<b>-c:v libx264:</b> Spécifie le codec vidéo à utiliser pour la sortie. Dans ce cas, le codec H.264 (libx264) est utilisé. Cela permet de réencoder la vidéo avec le codec H.264.

<b>-c:a copy:</b> Copie la piste audio de l'entrée vers la sortie sans réencoder. Si la source n'a pas de piste audio, cela n'affectera pas le résultat.

<b>/data/video2.mp4:</b> Chemin et nom du fichier de sortie MP4 où la vidéo résultante sera enregistrée.


<br>
<b>Il important de savoir que dans notre flow actuel, on capture le flux vidéo depuis deux caméra, donc dans votre cas par exemple le premier <b>Decode RTSP stream 2</b> on specifie l'adresse IP de la premiere caméra et pour le sécond <b>Decode RTSP stream 2</b> on spécifie l'adresse IP de la séconde caméra.</b>
 
</li>
  
</ul>

# Déploiement :
Après avoir effectué tous les prérequis ci dessus, il faut passer aux étapes suivant :
<ol type="1">
  <li>Déployer le flux avec le menu Node Red</li>
  <li>Connecter le pc et les smarphones sur le meme réseau</li>
  <li>Cliquer sur le noeud Start Network</li>
</ol>

La figure suivante décrit le flow déployé :

![Alt text](https://github.com/hamadouncisse/PROJECT_MTSC_NODE_RED/blob/main/Screenshot%20from%202024-01-22%2019-21-11.png "menu import")

# Démonstration :

La figure suivante décrit la détection d'une personne lors d'une capture de trame par les deux caméras IP :

![Alt text](https://github.com/hamadouncisse/PROJECT_MTSC_NODE_RED/blob/main/Screenshot%20from%202024-01-22%2019-22-43.png "menu import")

A partir de détection l'utilisateur récoit une notification via <b>Telegram</b> :

| Notification 1                            | Notification  2                        |
| ----------------------------------- | ----------------------------------- |
| ![Notification1](https://github.com/hamadouncisse/PROJECT_MTSC_NODE_RED/blob/main/Screenshot_2024-01-22-19-29-46-619_org.telegram.messenger.jpg) | ![notification2](https://github.com/hamadouncisse/PROJECT_MTSC_NODE_RED/blob/main/Screenshot_2024-01-22-19-30-30-071_org.telegram.messenger.jpg) |

La vidéo ci-dessus est la capture vidéo recu par l'utilisateur lors de la notification :

https://github.com/hamadouncisse/PROJECT_MTSC_NODE_RED/assets/104743493/2e5cb2b3-abe7-4068-81bc-81823f9251ba




