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

# ClientAndroid

Le client android se découpe en de multiples activités se découpant elles mêmes en de multiples fragments. Cette structure permet une meilleure expérience pour l'utilisateur. L'utilisation de ViewPager2 permet de proposer de multiples menus à l'horizontal à l'utilisateur.

Nous avons également utilisé la librairie [Lottie](https://github.com/airbnb/lottie-ios) qui nous permet d'afficher des sortes d'images animés sur l'écran. Particulièrement durant les chargements ou dans le menu principale pour l'image de fond.

Il est important également de parler de la librairie [LibGDX](https://github.com/libgdx/libgdx) sur laquel se repose beaucoup notre projet pour le jeu. Elle propose un portage sur Android pour afficher des modèles 3D complexes mais aussi une grande quantités de addons qui nous simplifie grandement la vie sur beaucoup de sujets.


# Activités

 <img src="https://raw.githubusercontent.com/For-The-Oil/.github/main/ressources/ActivitesEtFragments.png" alt="Listes des Activités et de leurs fragments" height="300">

## La SplashActivity
 <img src="https://raw.githubusercontent.com/For-The-Oil/.github/main/ressources/Splash_Activity.png" alt="Splash Activity" height="300">

## La LoginActivity

<img src="https://raw.githubusercontent.com/For-The-Oil/.github/main/ressources/LoginActivity_Login.png"  height="300"/>
<img src="https://raw.githubusercontent.com/For-The-Oil/.github/main/ressources/LoginActivity_Register.png"  height="300"/>
<img src="https://raw.githubusercontent.com/For-The-Oil/.github/main/ressources/LoginActivity_ServerSettings.png"  height="300"/>

## La HomeActivity

<img src="https://raw.githubusercontent.com/For-The-Oil/.github/main/ressources/HomeActivity_Main.png" alt="Splash Activity"  height="300">
<img src="https://raw.githubusercontent.com/For-The-Oil/.github/main/ressources/HomeActivity_DeckMenu.png" alt="Splash Activity"  height="300">
<img src="https://raw.githubusercontent.com/For-The-Oil/.github/main/ressources/HomeActivity_UnitsList.png" alt="Splash Activity"  height="300">
 <img src="https://raw.githubusercontent.com/For-The-Oil/.github/main/ressources/HomeActivity_Matchmaking.png" alt="Splash Activity"  height="300">

## La GameActivity

<img src="https://raw.githubusercontent.com/For-The-Oil/.github/main/ressources/GameActivity_Main.png" alt="Splash Activity"  height="300">
<img src="https://raw.githubusercontent.com/For-The-Oil/.github/main/ressources/GameActivity_PlacingBuilding.png" alt="Splash Activity"  height="300">
<img src="https://raw.githubusercontent.com/For-The-Oil/.github/main/ressources/GameActivity_Settings.png" alt="Splash Activity"  height="300">
