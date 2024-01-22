# PROJECT_MTSC_NODE_RED
Bienvenue dans notre solution de détection d'intrusion. Notre projet offre une réponse aux défis de surveillance en combinant l'intelligence des réseaux de caméras avec la flexibilité de Node-Red.
# AUTEURS - ETUDIANT M2 CNS SOUS PARCOURS SR
<ul>
  <li>CISSE Hamadoun</li>
  <li>LAIB Ramy</li>
  <li>SARAOUI Keltouma</li>
  <li>IWOBA REBET Emmanuel</li>
</ul>

# Principales fonctionnalités
<b>Détection d'Intrusion Intelligente :</b> Grâce au modèle de détection d'object (coco-ssd), notre système identifie de manière fiable les intrusions, garantissant une réaction proactive à toute menace potentielle.

<b>Notification Instantanée :</b> L'utilisateur est informé en temps réel dès qu'une activité suspecte est détectée, garantissant une réponse rapide et efficace.


<b>Visualisation en Direct :</b> Expérimentez la puissance de la visualisation en direct avec un accès immédiat à la sortie de la caméra concernée, offrant une compréhension visuelle précise de la situation en cours.

<b>Optimisation de traffic : </b> Notre système est concu de telle sorte à optimiser les trafics sur le réseau en réduisant au maximum les répétitions d'alertes liés à une meme intrusion.

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


<img src="![image](https://github.com/hamadouncisse/PROJECT_MTSC_NODE_RED/assets/104743493/3f8a5d6a-6f4f-4214-8898-4aef66c2c710)
" width="50%" height="50%">
<img src="https://github.com/hamadouncisse/PROJECT_MTSC_NODE_RED/assets/104743493/e0970096-a57d-4773-b7ff-a4232742560c" width="50%" height="50%">

  
</li>

  
</ul>

