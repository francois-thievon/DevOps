# Application Web Multi-Services avec Docker

## 📋 Description du Projet

Ce projet est un **TP DevOps** qui démontre la conteneurisation et l'orchestration d'une application web complète utilisant une architecture microservices. L'application consiste en un système de gestion d'étudiants et de départements avec une API REST, une base de données PostgreSQL et un serveur web Apache.

## 🏗️ Architecture de l'Application

L'application est composée de **4 services principaux** :

### 1. **Base de Données PostgreSQL** (`database`)
- **Image**: PostgreSQL 17.2 Alpine
- **Fonction**: Stockage des données des étudiants et départements
- **Port interne**: 5432
- **Schéma**: Tables `departments` et `students` avec relation one-to-many
- **Données de test**: Départements IRC, ETI, CGP avec plusieurs étudiants

### 2. **API Backend Spring Boot** (`backend`)
- **Framework**: Spring Boot 3.4.2 avec Java 21
- **Fonction**: API REST pour la gestion CRUD des étudiants et départements
- **Port**: 8080
- **Endpoints**:
  - `GET/POST/PUT/DELETE /students` - Gestion des étudiants
  - `GET/POST/PUT/DELETE /departments` - Gestion des départements
- **Base de données**: Connexion JPA/Hibernate avec PostgreSQL
- **Build**: Multistage Docker build (JDK pour compilation → JRE pour exécution)

### 3. **Serveur Web Apache** (`http_server`)
- **Image**: Apache HTTP Server 2.4
- **Fonction**: Serveur web frontend et reverse proxy
- **Port**: 80
- **Contenu**: Page d'accueil personnalisée

### 4. **Interface d'Administration** (`adminer`)
- **Image**: Adminer
- **Fonction**: Interface web pour administrer la base de données PostgreSQL
- **Port**: 8888

## 🐳 Containerisation

### Technologies utilisées
- **Docker** : Conteneurisation de chaque service
- **Docker Compose** : Orchestration des services
- **Multi-stage builds** : Optimisation des images Docker
- **Volumes** : Persistance des données PostgreSQL
- **Networks** : Communication inter-services

### Avantages de l'architecture
- **Isolation** : Chaque service dans son propre conteneur
- **Scalabilité** : Services indépendants facilement scalables
- **Portabilité** : Déploiement identique sur différents environnements
- **Maintenance** : Mise à jour indépendante de chaque service

## � CI/CD avec GitHub Actions

Ce projet implémente une pipeline **CI/CD complète** utilisant **GitHub Actions** pour automatiser :

### Pipeline d'Intégration Continue (CI)
- **Tests automatisés** : Exécution des tests unitaires et d'intégration du backend Spring Boot
- **Build des images Docker** : Construction automatique des images pour chaque service
- **Analyse de qualité de code** : Vérification du code avec des outils d'analyse statique
- **Tests de sécurité** : Scan des vulnérabilités dans les images Docker

### Pipeline de Déploiement Continue (CD)
- **Publication automatique** : Push des images Docker vers Docker Hub
- **Déploiement automatisé** : Mise à jour des services en production
- **Tests de smoke** : Vérification que l'application fonctionne après déploiement
- **Rollback automatique** : Retour à la version précédente en cas d'échec

### Déclencheurs
- **Push sur main** : Déploiement automatique en production
- **Pull Requests** : Tests et validation automatiques
- **Tags** : Création de releases versionnées

Cette approche **DevOps** garantit la qualité du code, la fiabilité des déploiements et la rapidité de mise en production des nouvelles fonctionnalités.

## �🚀 Utilisation

```bash
# Lancer tous les services
docker-compose up -d

# Construire les images
docker-compose build

# Arrêter les services
docker-compose down
```

### Accès aux services :
- **Application web** : http://localhost
- **API Backend** : http://localhost:8080
- **Adminer (DB Admin)** : http://localhost:8888

## 📚 Objectifs Pédagogiques

Ce TP permet d'apprendre :
- La conteneurisation d'applications multi-tiers
- L'orchestration avec Docker Compose
- Les bonnes pratiques Docker (multi-stage builds, volumes, networks)
- La gestion des variables d'environnement
- Le déploiement d'applications microservices
- L'utilisation de reverse proxy
- La persistance de données dans des conteneurs
- **L'implémentation de pipelines CI/CD avec GitHub Actions**
- **L'automatisation des tests, builds et déploiements**
- **La publication automatique d'images Docker sur Docker Hub**
- **Les stratégies de déploiement et de rollback**

## 🔗 Ressources

**Images Docker Hub** : https://hub.docker.com/u/francoisthievon

**Repository de correction** : https://github.com/FrancisLabrele/tp-devops-correction-docker.git

---

## 📝 Questions et Réponses du TP

### 1-1 Pourquoi utiliser le flag -e pour les variables d'environnement ?
L'utilisation du flag `-e` améliore la sécurité et la flexibilité en permettant de passer des variables sensibles au moment de l'exécution, plutôt que de les intégrer dans l'image Docker.

### 1-2 Pourquoi attacher un volume au conteneur PostgreSQL ?
Les conteneurs Docker sont éphémères. Monter un volume assure la persistance des données entre les redémarrages ou recreations du conteneur en stockant les fichiers de base de données sur la machine hôte.

### 1-3 Éléments essentiels du conteneur de base de données
Voir le Dockerfile dans le dossier Database. Construction d'une image de base de données personnalisée avec initialisation automatique du schéma et des données.

### 1-4 Pourquoi un build multi-stage ?
Le build multi-stage permet de réduire la taille de l'image finale et de l'optimiser. D'abord compilation avec JDK, puis création d'une image finale avec seulement JRE et l'artefact compilé.

### 1-5 Pourquoi un reverse proxy ?
Le reverse proxy gère les requêtes des clients et les redirige vers les services backend appropriés, permettant la répartition de charge et la sécurité.

### 1-6 Importance de Docker Compose
Docker Compose permet de définir et gérer facilement des applications multi-conteneurs avec un fichier YAML, simplifiant le déploiement et la gestion.

### 1-7 Commandes Docker Compose importantes
- `docker-compose build` : Construire les images
- `docker-compose up -d` : Démarrer les conteneurs en mode détaché
- `docker-compose down` : Arrêter et supprimer les conteneurs

### 1-8 Documentation du fichier docker-compose
Voir le fichier `docker-compose.yml` dans le repository qui définit l'orchestration complète des 4 services.

### 1-9 Publication sur Docker Hub
Images publiées et disponibles pour déploiement distant.

### 1-10 Pourquoi utiliser un registry en ligne ?
Permet de récupérer les images sur un serveur avec une simple connexion internet, facilitant le déploiement en production.
