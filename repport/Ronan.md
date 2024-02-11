# Rapport de Projet : SR Game

Cette page est un rapport de projet pour le projet SR Game, un jeu multijoueur en ligne développé dans le cadre du cours de Systèmes Répartis à l'ESIR.

Dans 


## Introduction
Dans le but de créer un jeu en ligne, nous nous sommes inspirés d'agar.io pour développer le jeu présent dans ce projet, un jeu multijoueur en ligne ou le but est de manger le plus possible de fruits disposés sur la carte,en dirigent des cellules dans une arène. 
Notre ambition était de fournir un jeu non seulement amusant mais aussi riche en défis techniques, notamment en programmation et en conception réseau.

## choix des technologies
Pour ce projet, nous avons choisi d'utiliser des technologies modernes et performantes.

### Frontend
Pour le développement frontend, nous avons opté pour Svelte, un framework JavaScript qui offre une expérience de développement fluide et réactive. J'étais en charge de cette partie, et j'ai également utilisé TailwindCSS pour la conception de l'interface utilisateur.

### Backend
Pour le développement backend, nous avons utilisé Spring Boot, un framework Java qui offre une grande flexibilité et une architecture solide. L'équipe backend a également intégré Websockets pour une communication en temps réel. J'ai participé à la logique de jeu et à la gestion des événements frontend-backend.


### Déploiement
Pour le déploiement, nous avons choisi Docker, qui offre une solution simple et efficace pour l'exécution de l'application. Nous avons également mis en place un système CD/CI pour l'automatisation du build des images sur github. Depuis un docker compose il est simple de déployer l'achitecture complète.

## Développement
Le développement du projet s'est déroulé en deux phases, chacune apportant des améliorations significatives au jeu.

## Développement en Phases

### Phase 1 : Infrastructure et Connexion
Initialement, nous avons établi l'infrastructure nécessaire, en mettant en place une connexion fiable entre les joueurs.
Ma contribution principale a été sur le développement frontend, créant une interface où les joueurs peuvent visualiser en temps réel qui est en ligne. Un simple leaderboard dont la logique sera retravaillée pour la suite pour être completement assimilée dans l'achitecture de la librairie de jeu.
Nous avons également implémenté un système CD/CI pour l'automatisation du déploiement et intégré Docker pour une exécution simplifiée.

### Phase 2 : Conception du Jeu
La seconde phase a vu le développement du cœur du jeu, introduisant une grille de déplacement et des éléments interactifs pour enrichir l'expérience de jeu. 
J'ai contribué à la partie frontend, assurant une expérience utilisateur fluide et réactive grâce à des technologies avancées comme Svelte et TailwindCSS.

## Architecture du Projet

Le projet repose sur une architecture client-serveur, séparant clairement frontend et backend. 
J'ai pris en charge le développement frontend, en m'assurant de fournir une interface utilisateur intuitive et réactive, facilitant l'interaction des joueurs avec le jeu.
L'utilisation de Websockets a été cruciale pour une communication en temps réel et l'intégration de Docker a simplifié le déploiement et la gestion du projet.

## Une librairie de jeu - fait maison

Frontend game lib : [GameEngine](https://github.com/SR-Distributed-Game/Frontend/tree/main/src/lib/GameEngine)

backend game lib : [GameEngine](https://github.com/SR-Distributed-Game/Backend/tree/main/src/main/java/org/esir/backend/GameEngine)

Pour faciliter le développement du jeu, nous avons créé une librairie de jeu réutilisable, qui gère la logique de jeu et la communication avec le backend. j'étais en charge de la conception de cette librairie. 

Je suis parti sur une architecture modulaire, avec des composants réutilisables.
Par exemple voila le composant attaché au player dans le frontend permettant le mouvement: 

- [playerMouvementComponent.ts](https://github.com/SR-Distributed-Game/Frontend/blob/main/src/lib/GameEngine/Components/PlayerMovementMouseComponent.ts)

When attached to a player by using addComponent methode, this component will allow the player to move with the mouse. It is simple to create component and attach them to a GameObject.

 Mon but était de fournir une interface simple. De ce constat je me suis basé sur l'implémentation de Unity. Cette librairie permet au developpeur de :

- Créer une instance de jeu
- Créer des Scenes personnalisées
- Gérer les événements de jeu tel que les collisions entre objets
- Créer des GameObjects personnalisés
- Créer des scripts pour les GameObjects

Par dessus cette librairie, il était alors simple d'ajouter une dimention multijoueur.

### multiplayer synchronisation

Pour interfacer les GameObjects et les Scenes entre le backend et le frontend, j'ai utilisé le processus de serialisation et de désérialisation.

Par exemple pour un Game object en typescript :
[GameObject.ts](https://github.com/SR-Distributed-Game/Frontend/blob/main/src/lib/GameEngine/GameObject.ts)

Son implémentation en Java :
[GameObject.java](https://github.com/SR-Distributed-Game/Backend/blob/main/src/main/java/org/esir/backend/GameEngine/GameObject.java)

Ce system permet de fermer la librairie à la modification, mais de l'ouvrir a l'extension.

Les classes permettant la simplicité de partage de variable entre le front et le back sont les classes suivantes : 

backend : 
- [SerializableJson](https://github.com/SR-Distributed-Game/Backend/blob/main/src/main/java/org/esir/backend/GameEngine/JsonSerializable.java)

- [SerializableGameObject](https://github.com/SR-Distributed-Game/Backend/blob/main/src/main/java/org/esir/backend/GameEngine/SerializableGameObject.java)

Frontend :

- [SerializableJson](https://github.com/SR-Distributed-Game/Backend/blob/main/src/main/java/org/esir/backend/GameEngine/JsonSerializable.java)


- [SerializableGameObject](https://github.com/SR-Distributed-Game/Frontend/blob/main/src/lib/GameEngine/SerializableGameObject.ts)


Une annotation permet également de définir quelles variables seront paragées entre le frontend et le backend.

```
@Serializable
```
Grace à de la reflection, les variables annotées seront partagées entre le frontend et le backend.


 Vous pouvez voir un exemple d'utilisation de cette annotation dans le code suivant :

- [player.ts](https://github.com/SR-Distributed-Game/Frontend/blob/main/src/lib/implementedGames/player.ts)

-[player.java](https://github.com/SR-Distributed-Game/Backend/blob/main/src/main/java/org/esir/backend/ImplementedGame/player.java)




## Conclusion

Le projet SR Game a atteint ses objectifs, en mettant en place une base solide dans sa première version et en enrichissant l'expérience de jeu dans la seconde. 
Grâce à une collaboration étroite entre les équipes backend et frontend, nous avons réussi à offrir un jeu en ligne dynamique et engageant. 
Mon implication sur le frontend a permis de garantir que les joueurs bénéficient d'une interaction fluide et immersive avec le jeu, posant ainsi les fondations pour des évolutions futures.
