# For The Oil  
## Jeu vidéo Android multijoueur 3D (Client / Serveur)

Projet réalisé par **Kenan Ammad** et **Gauthier Defrance**  
Lien du projet : https://github.com/For-The-Oil

---

## Sommaire
- [Présentation du projet](#présentation-du-projet)
- [Architecture générale](#architecture-générale)
- [Utilisation](#utilisation)
- [Serveur](#serveur)
- [Client Android](#client-android)
- [Architecture des activités](#architecture-des-activités)
  - [SplashActivity](#splashactivity)
  - [LoginActivity](#loginactivity)
  - [HomeActivity](#homeactivity)
  - [GameActivity](#gameactivity)

---

## Présentation du projet

**For The Oil** est un projet de jeu vidéo Android multijoueur en 3D, développé dans le cadre d’un projet universitaire (SAE – 2025, CY Paris Université).

Le projet repose sur :
- Un **client Android**
- Un **serveur applicatif Java TCP**
- Une **base de données PostgreSQL**
- Une architecture **client–serveur autoritaire**

Le serveur est le seul détenteur de la vérité :  
il valide les actions, synchronise les clients et empêche toute modification locale frauduleuse.  
Toutes les communications entre joueurs transitent obligatoirement par le serveur.

La communication réseau est assurée par la bibliothèque **KryoNET**, permettant l’échange d’objets sérialisés de manière performante.

---

## Architecture générale

- **Client Android**
  - Interface utilisateur
  - Rendu 3D
  - Envoi des actions joueur
- **Serveur Java**
  - Validation des actions
  - Synchronisation des états
  - Gestion des parties et des joueurs
- **Base de données PostgreSQL**
  - Comptes utilisateurs
  - Decks
  - Cartes débloquées
  - Statistiques

La base de données est hébergée chez **AlwaysData**.

---

## Utilisation

Un **serveur applicatif doit impérativement être lancé** pour pouvoir utiliser l’application.

Sans serveur :
- L’application ne pourra pas fonctionner correctement
- La connexion échouera systématiquement

Pour lancer votre propre serveur :
1. Recréez une base de données à partir du dossier `Database`
2. Modifiez le fichier de configuration du serveur
3. Lancez le serveur Java

Une fois le serveur actif :
- Renseignez l’IP et le port dans l’application
- Connectez-vous avec vos identifiants
- Accédez au jeu

---

## Serveur

Message attendu au démarrage du serveur :

<img src="https://raw.githubusercontent.com/For-The-Oil/.github/main/ressources/Booting_Server.png"
     alt="Console du serveur affichant le démarrage et l'initialisation"
     height="300">

Liste des commandes disponibles côté serveur :

<img src="https://raw.githubusercontent.com/For-The-Oil/.github/main/ressources/Server_AvailableCommands.png"
     alt="Liste des commandes disponibles sur le serveur"
     height="300">

### Technologies utilisées côté serveur

- **Jackson** – Sérialisation / désérialisation JSON  
- **PostgreSQL** – Base de données  
- **HikariCP** – Pool de connexions  
- **jBCrypt** – Hashage des mots de passe  
- **Artemis-ODB** – Architecture ECS (Entity Component System)

L’utilisation d’Artemis-ODB permet d’optimiser fortement les performances, aussi bien côté serveur que côté client.

---

## Client Android

Le client Android est structuré autour :
- De plusieurs **Activities**
- De nombreux **Fragments**
- De **ViewPager2** pour la navigation horizontale

Cette organisation améliore la lisibilité du code et l’expérience utilisateur.

### Bibliothèques principales

- **LibGDX**  
  - Rendu 3D
  - OpenGL ES
  - Gestion des modèles et scènes

- **Lottie**  
  - Animations vectorielles
  - Écrans de chargement
  - Fond animé du menu principal

---

## Architecture des activités

Schéma simplifié des activités et fragments :

<img src="https://raw.githubusercontent.com/For-The-Oil/.github/main/ressources/ActivitesEtFragments.png"
     alt="Schéma des activités Android et de leurs fragments"
     height="300">

---

## SplashActivity

La **SplashActivity** est affichée au lancement de l’application.

Fonctionnalités :
- Tentative de reconnexion automatique
- Vérification des identifiants
- Redirection vers l’écran de connexion en cas d’échec

<img src="https://raw.githubusercontent.com/For-The-Oil/.github/main/ressources/Splash_Activity.png"
     alt="Écran de démarrage de l'application Android"
     height="300">

---

## LoginActivity

La **LoginActivity** est composée de trois fragments :

### Connexion

<img src="https://raw.githubusercontent.com/For-The-Oil/.github/main/ressources/LoginActivity_Login.png"
     alt="Fragment de connexion utilisateur"
     height="300">

### Création de compte

<img src="https://raw.githubusercontent.com/For-The-Oil/.github/main/ressources/LoginActivity_Register.png"
     alt="Fragment de création de compte utilisateur"
     height="300">

### Paramètres serveur

<img src="https://raw.githubusercontent.com/For-The-Oil/.github/main/ressources/LoginActivity_ServerSettings.png"
     alt="Fragment de configuration du serveur"
     height="300">

---

## HomeActivity

La **HomeActivity** correspond à la phase de préparation avant la partie.

### Menu principal

Choix du mode de jeu et du deck actif.

<img src="https://raw.githubusercontent.com/For-The-Oil/.github/main/ressources/HomeActivity_Main.png"
     alt="Menu principal de la HomeActivity"
     height="300">

### Gestion des decks

Création, modification et visualisation des decks.

<img src="https://raw.githubusercontent.com/For-The-Oil/.github/main/ressources/HomeActivity_DeckMenu.png"
     alt="Menu de gestion des decks"
     height="300">

### Liste des unités

Affichage de toutes les entités du jeu.

<img src="https://raw.githubusercontent.com/For-The-Oil/.github/main/ressources/HomeActivity_UnitsList.png"
     alt="Liste complète des unités du jeu"
     height="300">

### Matchmaking

Attente de joueurs avant le lancement de la partie.

<img src="https://raw.githubusercontent.com/For-The-Oil/.github/main/ressources/HomeActivity_Matchmaking.png"
     alt="Écran d'attente du matchmaking"
     height="300">

---

## GameActivity

La **GameActivity** gère le déroulement de la partie.

- **LibGDXFragment** : rendu 3D OpenGL
- **Fragments UI** : HUD, menus, interactions

### Vue principale du jeu

<img src="https://raw.githubusercontent.com/For-The-Oil/.github/main/ressources/GameActivity_Main.png"
     alt="Vue principale du jeu en cours de partie"
     height="300">

### Placement d’un bâtiment

<img src="https://raw.githubusercontent.com/For-The-Oil/.github/main/ressources/GameActivity_PlacingBuilding.png"
     alt="Placement d'un bâtiment sur la carte"
     height="300">

### Menu des paramètres

<img src="https://raw.githubusercontent.com/For-The-Oil/.github/main/ressources/GameActivity_Settings.png"
     alt="Menu des paramètres en jeu"
     height="300">

---

## Sources & Références

### Bibliothèques et frameworks

- KryoNET  
  https://github.com/EsotericSoftware/kryonet  

- LibGDX  
  https://github.com/libgdx/libgdx  

- Artemis-ODB (Entity Component System)  
  https://github.com/junkdog/artemis-odb  

- Lottie (animations)  
  https://github.com/airbnb/lottie-android  

- Jackson (JSON)  
  https://github.com/FasterXML/jackson  

- PostgreSQL JDBC Driver  
  https://github.com/pgjdbc/pgjdbc  

- HikariCP (connection pool)  
  https://github.com/brettwooldridge/HikariCP  

- jBCrypt (hashage des mots de passe)  
  https://github.com/jeremyh/jBCrypt  

---

### Outils et services

- Android Studio  
  https://developer.android.com/studio  

- AlwaysData (hébergement base de données)  
  https://www.alwaysdata.com  

---

### Documentation officielle

- Android Developers  
  https://developer.android.com  

- OpenGL ES  
  https://www.khronos.org/opengles  

---

### Ressources graphiques

Les captures d’écran et assets visuels présents dans ce dépôt ont été réalisés dans le cadre du projet **For The Oil** et sont utilisés uniquement à des fins pédagogiques et démonstratives.

