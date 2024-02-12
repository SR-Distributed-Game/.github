# SR game


## Introduction
Dans le cadre de ce projet, nous ambitionnons de concevoir et de développer un jeu en ligne inspiré du célèbre agar.io, un jeu multijoueur massif où les joueurs contrôlent des cellules dans une arène, cherchant à consommer des cellules plus petites et à éviter d'être mangés par des cellules plus grandes. L'objectif de ce projet est de créer un jeu non seulement divertissant mais aussi technique, en intégrant des défis de programmation, de réseau et de conception de jeu.

La réalisation du projet se fera en deux versions principales, chacune avec des objectifs spécifiques, et chaque étape sera rigoureusement accompagnée de tests fonctionnels et unitaires pour assurer la qualité et la fiabilité des fonctionnalités développées :

### Version 1 : Infrastructure et Connexion des Joueurs

La première version du projet se concentrera sur la mise en place de l'infrastructure nécessaire au jeu et la gestion de la connexion des joueurs. Cette version inclura les fonctionnalités de base permettant à deux joueurs, sur des ordinateurs distincts, de se connecter à un serveur et de voir une liste des joueurs connectés sur une page blanche. Les objectifs principaux de cette version sont :

- La mise en place d'une page permettant d'afficher une liste des connexions en temps réel.
- La possibilité pour les joueurs de se connecter au serveur et de mettre à jour cette liste.
- L'implémentation d'un système de Continuous Deployment/Continuous Integration (CD/CI) pour automatiser le déploiement et l'intégration du code.
- La création automatique d'images Docker pour faciliter le déploiement et l'exécution du jeu.

L'acceptation de cette version sera validée par une démonstration du système fonctionnant sur deux ordinateurs différents, exécuté via une composition Docker.

### Version 2 : Création du Jeu

La deuxième version du projet se concentrera sur le développement de la logique du jeu proprement dite. Cette version introduira les mécanismes de jeu, tels que :

- Une grille permettant aux joueurs de se déplacer sans occuper la même case simultanément.
- La distinction visuelle entre les joueurs pour faciliter l'identification.
- La possibilité pour les joueurs de consommer des baies pour accumuler des points.
- L'implémentation d'un système de rollback pour gérer les interactions entre les joueurs et les éléments du jeu.
- L'ajout d'un système de priorité de déplacement, résolvant les conflits lorsque deux joueurs tentent de consommer la même baie simultanément.

Le déploiement de cette version du jeu sera effectué sur une machine virtuelle de l'ISTIC, utilisant Docker pour faciliter la mise en place et l'exécution.

L'acceptation de cette version sera démontrée par la capacité à exécuter le jeu sur la VM et à réaliser une démonstration sur deux ordinateurs distincts.

## Architecture
Ce projet repose sur une architecture client-serveur divisée en deux parties principales :le frontend et le backend. Cette structure permet une séparation claire entre la logique de présentation et la logique métier, favorisant ainsi une meilleure organisation du code, une maintenance simplifiée et une évolutivité accrue. Voici les éléments clés de l'architecture :

### Backend

Le backend agira comme le cœur logique du jeu, gérant les connexions des joueurs, la logique de jeu, et les interactions entre les joueurs. Il sera responsable de la synchronisation de l'état du jeu entre tous les joueurs connectés, assurant que chaque joueur ait une vue cohérente de l'arène de jeu.

### Frontend
Le frontend représentera l'interface utilisateur à travers laquelle les joueurs interagiront avec le jeu. Il sera conçu pour être réactif et dynamique, offrant une expérience utilisateur fluide et engageante. Les joueurs pourront voir la grille de jeu, se déplacer, et interagir avec les éléments de jeu comme les baies.

### Utilisation des Websockets

Pour permettre une communication en temps réel entre le frontend et le backend, nous utiliserons les Websockets. Cette technologie est cruciale pour assurer que les actions des joueurs soient instantanément répercutées sur tous les clients connectés, permettant ainsi une expérience de jeu interactive et synchronisée.


### Utilisation de Docker

Afin de faciliter le déploiement et la gestion de l'environnement de développement et de production, nous intégrerons Docker dans notre workflow. Docker nous permettra de créer des conteneurs pour le frontend et le backend, assurant que le jeu soit facilement déployable et exécutable dans n'importe quel environnement sans dépendre de configurations système spécifiques. Cela contribuera également à simplifier le processus de Continuous Integration/Continuous Deployment (CI/CD), permettant des mises à jour rapides et fiables du jeu.

## Architecture Frontend
### Explication de l'Architecture Frontend

L'architecture frontend sera conçue pour être légère, rapide et facilement adaptable, permettant une expérience utilisateur immersive et réactive. Elle se concentrera sur la facilitation de la communication en temps réel avec le backend, l'affichage efficace de l'état du jeu, et la gestion des interactions utilisateur. La structure sera modulaire, favorisant la réutilisabilité du code et une maintenance simplifiée.

![Frontend](./image/Fronted.png)

- Utilisation de Svelte
- Utilisation de Websockets
- Utilisation de TailwindCSS
- Création d'une Librairie de Jeu

## Architecture Backend
### Explication de l'Architecture Backend

L'architecture backend sera conçue pour être à la fois robuste et flexible, capable de gérer les interactions complexes entre les joueurs et le système de jeu en temps réel. Pour cela, elle sera composée de plusieurs composants clés travaillant de concert pour traiter les requêtes des joueurs, exécuter la logique de jeu, et maintenir l'état du jeu à jour et synchronisé à travers tous les clients connectés.

![Backend Architecture](./image/Diagramme%20sans%20nom.drawio.png)

### Utilisation de Spring Boot

Nous utiliserons Spring Boot comme framework principal pour développer le backend. Spring Boot est choisi pour sa capacité à simplifier le développement d'applications Java, grâce à son système d'auto-configuration et à son vaste écosystème de modules. Il facilite notamment la gestion des connexions WebSocket, la mise en place d'une architecture en microservices.

### Utilisation de Websockets

Pour permettre une communication bidirectionnelle en temps réel entre le serveur et les clients, le backend utilisera des Websockets. Ce choix est essentiel pour des jeux en ligne nécessitant des mises à jour immédiates de l'état du jeu, comme la position des joueurs, les interactions et les scores. Spring Boot offre un support solide pour les Websockets, ce qui permettra une intégration facile et efficace de cette technologie dans notre architecture.


### Création d'une Librairie de Jeu

Pour gérer la logique de jeu spécifique, comme le mouvement des joueurs, la génération des baies, et le scoring, nous développerons une librairie de jeu dédiée. Cette librairie sera conçue pour être modulaire et réutilisable, permettant une évolution facile du jeu et la possibilité d'ajouter de nouvelles fonctionnalités ou de modifier la logique de jeu existante sans impacter négativement l'architecture globale. L'intégration de cette librairie au sein du projet Spring Boot permettra une gestion efficace de la logique de jeu, en s'appuyant sur les principes de programmation orientée objet et les fonctionnalités de Spring pour une intégration transparente.


## Contributions Personnelles
Voici les points sur lesquels j'ai personnellement œuvré :
### Déploiement

J'ai pris en charge le déploiement de l'application, en m'assurant que toutes les composantes du jeu soient correctement configurées et opérationnelles dans l'environnement de production. Cela a inclus la gestion des conteneurs Docker, la configuration des services, et l'assurance d'une intégration fluide entre le frontend et le backend.
### Architecture du Backend

J'ai conçu l'architecture du backend, en sélectionnant Spring Boot pour son efficacité et sa facilité d'utilisation. Mon travail a été crucial dans la mise en place d'une structure solide permettant une communication en temps réel et la gestion efficace de la logique de jeu, tout en assurant la scalabilité et la maintenabilité du système.
### Le Load Testing

Pour garantir la fiabilité et la performance du jeu sous différentes charges d'utilisation, j'ai effectué des tests de charge approfondis. Ces tests ont permis d'identifier et de corriger les goulets d'étranglement, assurant ainsi une expérience utilisateur fluide même lors de pics d'utilisation.
### Le Décodage et Encodage des Messages

J'ai développé la logique d'encodage et de décodage des messages échangés entre le client et le serveur, permettant une communication efficace et sécurisée. Cette contribution a été fondamentale pour le bon fonctionnement des Websockets et la synchronisation de l'état du jeu entre tous les joueurs.
### Rendre Threadable les Encodeurs/Décodeurs

Pour optimiser les performances et la réactivité du jeu, j'ai rendu les encodeurs et décodeurs threadables. Cette amélioration technique a significativement réduit les temps de latence dans le traitement des messages, contribuant ainsi à une meilleure expérience de jeu en temps réel.


## Conclusion

En conclusion, nous avons respecté toutes les exigences initiales, en développant un jeu qui non seulement correspond à la vision que nous avions au départ mais qui apporte également de nouvelles fonctionnalités.

La première version a établi une base solide avec une infrastructure permettant aux joueurs de se connecter et d'interagir en temps réel, grâce à l'utilisation judicieuse de technologies comme Docker et les Websockets. Ensuite, la deuxième version a introduit la véritable essence du jeu, avec une grille de mouvement, des éléments interactifs, et une expérience utilisateur fluide, le tout rendu possible par notre choix d'utiliser Svelte et TailwindCSS pour le frontend.

Au final, non seulement nous avons réussi à créer un jeu fonctionnel, mais nous avons également mis en place une architecture robuste et flexible, prête pour des évolutions futures.

