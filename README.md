# Paris Film Shooting — Web Application

Mini-projet - de la modélisation à la visualisation 
ZHAO Qichao

---

## 1. Présentation du projet

Ce projet est basé sur le jeu de données open data de la Ville de Paris **« Lieux de tournage à Paris »**.
Il couvre l’ensemble du processus, depuis la modélisation sémantique (RDFS) et la construction du graphe RDF, jusqu’aux requêtes SPARQL et à la visualisation Web des données.

Objectifs du projet :

* Transformer les données initiales en RDF (format Turtle)
* Construire un schéma RDFS
* Déployer les données sur Apache Jena Fuseki
* Interroger les données dynamiquement avec SPARQL
* Visualiser les données avec D3.js et Leaflet


---

## 2. Structure du dépôt

Le dépôt actuel contient :

```
.
├── schema.ttl
├── instance.ttl
├── web_index.html
├── ZHAO_Qichao.pdf
└── README.md
```

Description des fichiers :

* **schema.ttl**
  Définit le schéma RDFS, incluant les classes, les propriétés, les domain, les range ainsi que les alignements LOD.

* **instance.ttl**
  Données RDF d’instances (individus de FilmShooting ainsi que leurs informations de lieu, de période et de géométrie).

* **web_index.html**
  Application Web côté client (requêtes SPARQL + visualisation avec D3 et Leaflet).

* **ZHAO_Qichao.pdf**
  Rapport complet du projet (incluant le processus de modélisation, l’explication des requêtes SPARQL, ainsi que des captures d’écran de l’interface).

* **README.md**
  Introduction au projet et manuel d'utilisation.

---

## 3. Source des données

Source des données :

Open Data Paris

Nom du jeu de données :
**Lieux de tournage à Paris**

Page officielle :
https://opendata.paris.fr/explore/dataset/lieux-de-tournage-a-paris/information/?disjunctive.type_tournage&disjunctive.nom_tournage&disjunctive.nom_realisateur&disjunctive.nom_producteur&disjunctive.ardt_lieu


---

## 4. Description de la modélisation RDF

### 4.1 Classes (schema.ttl)

Les classes principales définies sont :

* :FilmShooting
* :IdentifiantLieu
* :Geometrie
* :Localisation
* :PeriodeTournage

La classe **:FilmShooting** constitue la classe centrale du modèle et représente un événement de tournage.

---

### 4.2 Propriétés

Les principales propriétés définies sont :

* :Titre
* :Année_du_tournage
* :Type_de_tournage
* :Producteur
* :nomRealisateur
* :aIdentifiantLieu
* :aPeriodeTournage
* :aPourRealisateur (alignement avec Wikidata)
* :seSitueDans (lien vers wd:Q90 – Paris)

La modélisation repose sur **RDFS uniquement** (sans utilisation d’OWL ni de mécanismes d’inférence).


---

### 4.3 Structure des données d’instances (instance.ttl)

Chaque **:FilmShooting** contient :

* l’année du tournage
* le type de tournage
* le réalisateur
* l’adresse
* le code postal
* les coordonnées géographiques (geoPoint2D)
* la période de tournage
* un lien vers Wikidata

Les informations de localisation sont organisées à l’aide d’une structure en **blank nodes** :

FilmShooting
→ IdentifiantLieu
→ Geometrie
→ Localisation

---

## 5. Architecture technique

* RDF / RDFS
* Apache Jena Fuseki
* SPARQL
* JavaScript
* D3.js
* Leaflet
* Leaflet.markercluster
* Leaflet.heat

---

## 6. Étapes de lancement

### Étape 1 : Démarrer Fuseki

Lancer le serveur Fuseki :

```
.\fuseki-server.bat
```

Ouvrir l’interface d’administration :

```
http://localhost:3030/
```

---

### Étape 2 : Créer un Dataset

Créer un dataset, par exemple :

```
lieux-de-tournage-a-paris
```

---

### Étape 3 : Charger les données RDF

Charger les deux fichiers suivants dans le même Named Graph :

* schema.ttl
* instance.ttl

URI recommandée pour le Named Graph :

```
http://zqc/paris-shooting/graph
```

---

### Étape 4 : Lancer la page Web

Double-cliquer directement sur `web_index.html`.

---

## 7. Configuration SPARQL par défaut

La page utilise par défaut :

SPARQL Endpoint :

```
http://localhost:3030/lieux-de-tournage-a-paris/query
```

Named Graph :

```
http://zqc/paris-shooting/graph
```

Si le nom du dataset est différent, veuillez modifier l’endpoint en haut de la page.


---

## 8. Description des fonctionnalités Web

### 8.1 Requêtes SPARQL dynamiques

Les filtres suivants sont pris en charge :

* Intervalle d’années
* Type de tournage (valeurs multiples possibles)
* Recherche par mot-clé dans le titre
* Code postal (valeurs multiples possibles)
* Option pour afficher uniquement les enregistrements contenant un alignement Wikidata
* Limitation du nombre de résultats (LIMIT)

La page permet d’afficher et de consulter la requête SPARQL générée automatiquement.

---

### 8.2 Visualisation cartographique (Leaflet)

Trois modes d’affichage sont disponibles :

* Cluster (mode de regroupement des points)
* Heatmap (mode carte thermique)
* Plain (mode points simples)

La carte interprète automatiquement les coordonnées de Paris à partir du champ **geoPoint2D**.


---

### 8.3 Analyse statistique (agrégations SPARQL)

Les agrégations sont réalisées à l’aide de **COUNT** et **GROUP BY** :

* Nombre de tournages par année (courbe de tendance)
* Nombre de tournages par type (diagramme en barres)
* Répartition des types (diagramme circulaire)
* Distribution par code postal (diagramme en barres)

Les données statistiques sont obtenues via des requêtes SPARQL d’agrégation distinctes.

---

## 9. Alignement LOD

Ce projet met en œuvre un alignement avec le Linked Open Data :

* Paris → wd:Q90
* Réalisateurs → entités Wikidata
* Films → entités Wikidata

En cliquant sur une ligne du tableau, il est possible d’afficher dans le panneau latéral les informations détaillées provenant de Wikidata.

---

## 10. Rapport

Le rapport complet du projet est disponible dans :

ZHAO_Qichao.pdf

Le rapport contient :

* La source des données
* Les étapes de modélisation des données
* Le squelette RDF (OpenRefine)
* La description du schéma
* Des extraits du fichier RDF
* Les requêtes SPARQL utilisées
* Des captures d’écran de l’interface
* L’explication des parties de code générées ou assistées par un LLM

---

## 11. Auteur

ZHAO Qichao



