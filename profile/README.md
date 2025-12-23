# **For The Oil**
## Projet de jeu vidéo Android multijoueur en 3D
_Projet par Kenan Ammad et Gauthier Defrance_
lien vers le **[Github](https://github.com/For-The-Oil)**

# Sommaire
- [Introduction](#introduction)
- [Utilisation](#utilisation)
- [Serveur](#serveur)
- [Client Android](#clientAndroid)
- [Activités](#activités)


# Introduction

Ce projet ressemble grandement à notre projet de SAE, fait cette 2025 dans le cours de M. Lemaire à CY Paris Université. Il consiste en la mise en place d'un client applicatif, serveur applicatif et une base de donnée ( il y a également une partie web, mais peu pertinente pour ce projet).
Nous avons donc mis en place cela, le client applicatif correspond donc à notre application android qui se connecte donc à un serveur Java TCP classique. Nous utilisons la librairie [KryoNET](https://github.com/EsotericSoftware/kryonet) pour simplifier la communication et l'échange d'objet sérialisé.

Nous utilisons donc une structure de serveur authoritaire, ou seul lui détient la vérité. Il sert à vérifier les informations des clients et les synchroniser. Tout échanges entre clients passe obligatoirement par le serveur.

Pour la partie base de donnée nous utilisons une simple base de donnée PosteGreSQL hébérgé gratuitement chez [AlwaysData](https://www.alwaysdata.com/fr/). Nous y stockons des informations relative au joueur tel que son pseudo, mail, mot de passe hashé... Mais aussi des informations concernant par exemple les cartes qu'il a débloqué en jeu et les decks qu'il possède.

# Utilisation

Il est **impératif** pour pouvoir utiliser correctement l'application d'avoir un serveur applicatif de lancer. Vous ne pourrez en conséquence probablement pas le lancer vous même malheureusement à moins de recréer votre propre base de donnée à partir des fichiers dans le repo Database du projet. Vous devrez alors modifier le fichier config de votre serveur afin qu'il s'y connecte au démarrage.

En supposant que vous avez bien un serveur de déjà lancé, vous aurez juste à entrer le port et IP de votre serveur, puis vous authentifier pour avoir accès au jeu.

# Serveur

Voici le message que vous devriez recevoir au démarrage de votre serveur

<img src="https://raw.githubusercontent.com/For-The-Oil/.github/main/ressources/Booting_Server.png" alt="Booting Server"  height="300">

et ici, la liste des commandes disponible pour le serveur

<img src="https://raw.githubusercontent.com/For-The-Oil/.github/main/ressources/Server_AvailableCommands.png" alt="Server Available Commands" height="300">

Cotés serveur, nous avons utilisé les librairies, [jackson](https://github.com/FasterXML/jackson) pour tout ce qui concerne la sérialisation et désérialisation de JSON, nous avons utilisé [postgresql](https://github.com/pgjdbc/pgjdbc) avec [HikariCP](https://github.com/brettwooldridge/HikariCP) et [jbcrypt](https://github.com/jeremyh/jBCrypt) pour toute la partie base de données et cryptage des informations.

Mais surtout, nous utilisons [Artemis-ODB](https://github.com/junkdog/artemis-odb) qui est une librairie implémentant le modèle ECS extrêmement utile dans son fonctionnement pour augmenter les performances du serveur et du client.

# ClientAndroid

Le client android se découpe en de multiples activités se découpant elles mêmes en de multiples fragments. Cette structure permet une meilleure expérience pour l'utilisateur. L'utilisation de ViewPager2 permet de proposer de multiples menus à l'horizontal à l'utilisateur.

Nous avons également utilisé la librairie [Lottie](https://github.com/airbnb/lottie-ios) qui nous permet d'afficher des sortes d'images animés sur l'écran. Particulièrement durant les chargements ou dans le menu principale pour l'image de fond.

Il est important également de parler de la librairie [LibGDX](https://github.com/libgdx/libgdx) sur laquel se repose beaucoup notre projet pour le jeu. Elle propose un portage sur Android pour afficher des modèles 3D complexes mais aussi une grande quantités de addons qui nous simplifie grandement la vie sur beaucoup de sujets.


# Activités

Ici, vous pouvez lire la liste des activités et leurs fragments pour une meilleur compréhension de la structure simplifier de notre application.

 <img src="https://raw.githubusercontent.com/For-The-Oil/.github/main/ressources/ActivitesEtFragments.png" alt="Listes des Activités et de leurs fragments" height="300">

## La SplashActivity

La **SplashActivity** est celle qui apparaît au démarrage du client. Si vous avez activé l'auto connection, alors elle tentera de se connecter automatiquement au dernier serveur enregistré avec les identifiants enregistré.
En cas d'échec ou autres, vous serez simplement rediriger vers la page de connection avec une message d'erreur au cas ou un problème est survenu.

 <img src="https://raw.githubusercontent.com/For-The-Oil/.github/main/ressources/Splash_Activity.png" alt="Splash Activity" height="300">

## La LoginActivity

La **LoginActivity** se découpe en 3 fragments.

Tout d'abord, le fragment de connexion classique, qui suppose que vous avez déjà un compte.

<img src="https://raw.githubusercontent.com/For-The-Oil/.github/main/ressources/LoginActivity_Login.png"  height="300"/>

Ensuite, le fragment de création de compte. Permettant à un utilisateur de s'authentifier.

<img src="https://raw.githubusercontent.com/For-The-Oil/.github/main/ressources/LoginActivity_Register.png"  height="300"/>

Finalement, il est également possible pour l'utilisateur de modifier les paramètres de connexion au serveur applicatif.

<img src="https://raw.githubusercontent.com/For-The-Oil/.github/main/ressources/LoginActivity_ServerSettings.png" height="300"/>


## La HomeActivity

Concernant la **HomeActivity**, c'est ici que se déroule la préparation au jeu.

Dans le Main Fragment, le client choisira ici le mode de jeu qu'il souhaite rejoindre et pourra alors lancer la partie. Il est possible d'y visualiser quel Deck nous avons sélectionné.

<img src="https://raw.githubusercontent.com/For-The-Oil/.github/main/ressources/HomeActivity_Main.png" alt="Splash Activity"  height="300">

Dans le Deck Fragment il est possible de constituer son Deck mais aussi de créer un nouveau Deck qu'on nommera alors. On peut y voir toutes les cartes qu'on a débloqué. Mais aussi leurs informations.

<img src="https://raw.githubusercontent.com/For-The-Oil/.github/main/ressources/HomeActivity_DeckMenu.png" alt="Splash Activity"  height="300">

Dans ce menu, on peut y voir la liste de toutes les entités existantes dans notre jeu.

<img src="https://raw.githubusercontent.com/For-The-Oil/.github/main/ressources/HomeActivity_UnitsList.png" alt="Splash Activity"  height="300">

Finalement, ce menu apparaît quand le joueur est en attente d'un matchmaking.

 <img src="https://raw.githubusercontent.com/For-The-Oil/.github/main/ressources/HomeActivity_Matchmaking.png" alt="Splash Activity"  height="300">

## La GameActivity

La **GameActivity** gère l'affichage du jeu et son déroulement.

Le fragment principal est le **LibGDXFragment**, on peut l'appercevoir dans le fond. C'est lui qui affiche le rendu des calculs de OpenGL ES. Par dessus, on a un autre Fragment qui est le Main. Il sert pour l'affichage du HUD.

<img src="https://raw.githubusercontent.com/For-The-Oil/.github/main/ressources/GameActivity_Main.png" alt="Splash Activity"  height="300">

Ici un exemple de l'utilisateur qui est en train de placer un batîment en jeu.

<img src="https://raw.githubusercontent.com/For-The-Oil/.github/main/ressources/GameActivity_PlacingBuilding.png" alt="Splash Activity"  height="300">

et enfin ici, un exemple de l'utilisateur en train d'accéder au menus des paramètres pour quitter le jeu par exemple.

<img src="https://raw.githubusercontent.com/For-The-Oil/.github/main/ressources/GameActivity_Settings.png" alt="Splash Activity"  height="300">
