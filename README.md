Synthèse des Projets du Parcours Data Engineer

I. Description Détaillée des Projets et Outils
1. Projet d'Audit de Données (SuperSmartMarket)
Description : La mission consistait à enquêter sur des incohérences dans le Chiffre d'Affaires (CA) d'une chaîne de supermarchés, qui variait d'un jour à l'autre dans le tableau de bord PowerBI. L'analyse a été menée sur une base de données OLAP.

Outils Utilisés :

SQL : Requêtes pour l'analyse des tables, le calcul du CA et la vérification des transactions.

Modélisation/Documentation : Création du Dictionnaire de données et du Schéma Relationnel.

Résultats Obtenus :

Identification de deux sources d'incohérence :

Historique des prix non sécurisé : Le CA était recalculé en utilisant les prix mis à jour, faussant l'historique des transactions.

Chargement de données différé : Un lot de 1379 transactions de la veille a été inséré le jour suivant (jour de fermeture), amplifiant l'écart de CA.

Recommandations : Sécuriser les prix historiques (stockage du prix de vente dans la table des transactions), contrôler le processus de chargement des ventes et mettre en place un monitoring des anomalies.

2. Projet de Base de Données Relationnelle (Laplace Immo)
Description : Dans le cadre de l'expansion d'un réseau immobilier, l'objectif était de collecter des données de transactions immobilières pour suivre le prix au mètre carré et identifier les régions les plus porteuses.

Outils Utilisés :

SQL : Utilisé pour la modélisation (création des tables commune géographie, communes démographie, transactions foncières) et l'interrogation pour répondre aux besoins métier.

Résultats Obtenus : Réponse à 11 problématiques métier via SQL, telles que :

Nombre total d'appartements vendus au 1er semestre 2020.

Liste des 10 départements avec le prix au mètre carré le plus élevé.

Taux d'évolution du nombre de ventes entre trimestres.

Classement des régions selon le prix au mètre carré des appartements de plus de 4 pièces.

3. Projet de Streaming de Données (InduTech)
Description : Conception d'une preuve de concept (PoC) pour un système de gestion de tickets clients en temps réel, utilisant un broker de messages et un moteur de traitement Big Data.

Outils Utilisés :

Redpanda (Kafka) : Broker de messages pour l'ingestion de données en continu.

PySpark (Spark Streaming) : Moteur pour le traitement et l'analyse des flux de données en temps réel.

Docker/Docker Compose : Conteneurisation des services.

AWS S3 : Choix justifié pour le stockage des données non structurées (logs, données brutes).

Format Parquet : Utilisé pour l'exportation des résultats d'analyse (efficacité Big Data).

Résultats Obtenus :

Mise en place d'un pipeline fonctionnel (Producteur -> Redpanda -> PySpark).

Réalisation d'une agrégation par fenêtre glissante de 1 minute (sliding window) pour calculer le nombre total de tickets par priorité.

Exportation des résultats agrégés au format Parquet pour l'archivage et l'analyse différée.

4. Projet d'Orchestration ETL (BottleNeck)
Description : Transformation d'un processus manuel de nettoyage et d'analyse de données (produits et ventes de vin) en un workflow automatisé et robuste à l'aide d'un orchestrateur.

Outils Utilisés :

Kestra : Outil d'orchestration pour séquencer les tâches.

DuckDB : Base de données analytique in-memory pour le nettoyage, la jointure et les agrégations via SQL.

Cron : Planification de l'exécution du workflow (le 15 de chaque mois à 9h).

Résultats Obtenus :

Conception et implémentation d'un workflow Kestra incluant le nettoyage, la réconciliation et le calcul du CA.

Intégration de tâches de tests de qualité après chaque étape de transformation (doublons, valeurs manquantes, cohérence des jointures, cohérence du CA, Z-score sur les prix des vins).

Production des extractions finales (CA par produit, listes de vins Premium/Ordinaires).

Mise en place d'une solution pour la gestion des dysfonctionnements (indisponibilité de DuckDB).

5. Projet d'Infrastructure Cloud et ELT (GreenCoop)
Description : Construction d'une infrastructure de données complète sur AWS pour ingérer et enrichir des relevés météorologiques hétérogènes et assurer leur qualité pour les Data Scientists.

Outils Utilisés :

AWS Fargate : Service de calcul sans serveur pour l'exécution des conteneurs.

Airbyte : Outil ELT utilisé pour la réplication des données (du S3 vers une destination MongoDB).

AWS S3 : Stockage des données brutes météorologiques.

MongoDB : Base de données cible (destination) pour les données enrichies.

AWS CloudWatch : Configuration du monitoring et des alarmes critiques (ex: Alarme Disque Plein).

AWS Backup : Planification des sauvegardes de volumes EBS.

Résultats Obtenus :

Mise en place d'un pipeline ETL Cloud natif et entièrement surveillé sur AWS.

Configuration d'Airbyte pour le flux de données.

Implémentation d'un audit de qualité des données en Python (quality_audit.py).

Assurance de la pérennité et de la fiabilité de l'infrastructure via le monitoring et les plans de sauvegarde.

6. Projet NoSQL et MLOps (Seattle)
Description : Développement d'un modèle de Machine Learning pour prédire l'Intensité des émissions de gaz à effet de serre (GES) des bâtiments et mise à disposition de ce modèle via une API web conteneurisée.

Outils Utilisés :

Python/ML : Développement du modèle de prédiction.

FastAPI : Développement de l'API RESTful pour servir le modèle.

BentoML : Encapsulation du modèle et de l'API dans une image Docker pour le déploiement.

Pydantic/Pandera : Validation stricte des données entrantes de l'API pour garantir la qualité.

Google Cloud Platform (GCP) : Déploiement de l'API.

Résultats Obtenus :

Modèle de ML opérationnel.

API RESTful fonctionnelle avec documentation Swagger UI (http://localhost:8000/docs).

Garantie de l'intégrité des données grâce à la validation à l'entrée de l'API.

Déploiement réussi sur le Cloud (GCP) pour une utilisation publique.

7. Projet de Sharding MongoDB (NosCités)
Description : Suite à un crash de la base de données de Paris, la mission consistait à restaurer, analyser l'intégrité de la sauvegarde, et pérenniser l'utilisation de la base de données.

Outils Utilisés :

MongoDB : Base de données NoSQL.

MongoDB Compass : Outil de visualisation et de gestion du cluster.

Docker/Docker Compose : Conteneurisation.

Migration Python : Script pour la migration de données médicales (dans le projet connexe "Migration & Docker").

Résultats Obtenus :

Restauration de la base de données à partir de la sauvegarde.

Mise en place d'une architecture Sharded Cluster pour garantir la pérennité, la haute disponibilité et l'évolutivité.

Création de deux shards (par exemple parisReplSet et lyonReplSet) et configuration d'un routeur mongos pour la distribution des requêtes.

Démonstration de l'optimisation des requêtes grâce au sharding (une requête sur Paris n'interroge pas le shard de Lyon).

Définition de la sécurité des rôles (Admin, Opérateur, Spectateur).

II. Compétences Démontrées et Valeur Ajoutée
L'ensemble de ces projets démontre une maîtrise complète du cycle de vie des données, des fondations à l'exploitation en production.

Compétences Techniques Démontrées
Maîtrise de la Base de Données (SQL/NoSQL) :

Modélisation (Schéma Relationnel, OLAP/OLTP).

Optimisation et Analyse de données (requêtes complexes, Data Mining).

Expertise NoSQL (MongoDB Sharding, réplication, avantages NoSQL).

Ingénierie de Données (Data Engineering) :

Conception et Automatisation de Pipelines ETL/ELT (Airbyte, Kestra).

Traitement Big Data & Streaming (PySpark, Redpanda/Kafka, agrégations par fenêtre).

Qualité des Données (Détection d'anomalies, validation Pydantic/Pandera, intégration de tests dans les workflows).

DevOps & Cloud (MLOps) :

Conteneurisation et Orchestration (Docker, Docker Compose).

Déploiement Cloud (AWS Fargate, AWS S3, GCP).

Surveillance et Résilience (AWS CloudWatch, AWS Backup, gestion des échecs Kestra).

Intelligence Artificielle (AI/MLOps) :

Développement d'API (FastAPI) pour l'exposition de modèles.

Architecture RAG (LangChain, Faiss) pour le développement d'assistants intelligents.

Valeur Ajoutée en tant que Data Engineer
Fiabilité des Données : Capacité à auditer des systèmes existants (Audit SuperSmartMarket) et à identifier les failles (prix non historisés, chargement asynchrone) pour proposer des solutions concrètes et pérennes.

Automatisation et Efficacité : Expertise dans la mise en place de systèmes d'orchestration (Kestra) pour transformer des processus manuels en workflows planifiés et fiables, intégrant la qualité des données comme une étape essentielle du pipeline.

Scalabilité et Temps Réel : Capacité à concevoir des architectures distribuées (Sharding MongoDB, PySpark/Redpanda) adaptées à de grands volumes de données et aux exigences de traitement en temps réel.

Sécurité et Conformité : Prise en compte de la sécurité (rôles utilisateurs, authentification) et de la résilience (monitoring CloudWatch, plans de sauvegarde AWS) dès la conception de l'infrastructure.

Innovation : Intégration des technologies émergentes (Bases de données vectorielles, LLM, MLOps) pour créer de la valeur métier (recommandation d'événements, prédiction de GES).
