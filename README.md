# Versailles Hackathon - Base Prosocour : Analyse de Réseaux de Sociabilité

## 📋 Description du Projet

Ce projet Hackathon en collaboration avec le Centre de recherches du Château de Versailles vise à **modéliser et analyser les réseaux de sociabilité de la cour royale** à travers une base de données prosopographique complète. L'objectif est de transformer des données complexes en visualisations pertinentes et en analyses reproductibles du tissu social, des institutions et des dynamiques relationnelles du Grand Siècle (17e siècle).

### Contexte

**ProsoCours** est une base de données enrichie contenant des informations sur :
- Les **personnes** de la cour (identifiants, attributs sociologiques)
- Les **charges et institutions** (hiérarchie administrative, maisons royales)
- Les **liens interpersonnels** (familiaux, professionnels, religieux)

Le défi lancé par le Centre du Château de Versailles était d'explorer cette data en profondeur pour :
1. Produire des **analyses diachroniques** structurées
2. Générer des **visualisations lisibles** argumentées
3. Démontrer la **pertinence historique** des résultats
4. Proposer des méthodes **reproductibles et scalables**

---

## 👥 Répartition du Travail

### **Juliette G. & Côme P.**
- **Modélisation d'une base de données nettoyée** : Création d'une base "pure" en filtrant les données sourcées
- **Analyses de réseaux diachroniques** : Étude temporelle des évolutions du tissu social
- **Production de statistiques structurées** : Agrégation par institutions avec ventilation démographique
- Exports : CSV statistiques, graphiques institutionnels sourcés

### **Martin H.**
- **Modélisation des données brutes** : Traitement direct de la base complète (non filtrée)
- **Analyses réseau exhaustives** : Applications de méthodes de théorie des graphes
- **Visualisations exploratoires** : Graphes en cosmogonie, réseaux professionnels, familiaux et religieux
- **Calcul de métriques** : Centralité (degree, betweenness), détection de communautés

### **Julie D.**
- **Modélisation mathématique et statistique** : Approche quantitative globale du dataset
- **Analyses de distribution** : Analyse des attributs (sexe, noblesse, logement) par institution
- **Études de corrélation** : Relations entre variables sociologiques et positions réseau
- **Métriques agrégées** : Calculs de coefficients, proportions et tendances

### **Juliette G., Côme P., Martin H., Julie D.**
- **Compréhension et nettoyage du dataset** : Le dataset était complexe et partiellement brut
- **Travail d'historiens** : Validation des résultats au regard des connaissances thématiques du Grand Siècle
- **Pertinence des analyses** : Discussions collectives pour assurer la cohérence historique

---

## 📊 Données et Méthodologie

### Sources de Données

#### **Base Brute (Données Brutes/)**
- `Prosocour_données_brutes.ipynb` : Traitements exploratoires sur l'intégralité de la base
- Format : JSON Lines (JSONL)
- Contient l'ensemble des personnes, charges et liens sans filtrage

#### **Base Sourcée (Données Pures/)**
- `Prosocours_sources.ipynb` : Base nettoyée - uniquement les enregistrements validés par une source
- Filtrage : Conservation des liens et charges pourvus de références bibliographiques
- Plus fiable mais plus restrictive

#### **Données Statistiques**
- `institutions_stats_percentages.csv` : Tableau agrégé des institutions
  - **Colonnes** : Institution, Niveau hiérarchique, Total d'effectifs
  - **Ventilation démographique** : % homme/femme, % logé/non-logé, % noble/non-noble
  - **728 lignes** : Couvre l'ensemble des institutions de la Maison du Roi et de la Reine

### Méthodes Computationnelles

#### **1. Théorie des Graphes**
```python
# Construction de graphes réseaux avec NetworkX
import networkx as nx

# Nœuds : Individus
# Arêtes : Relations (familiales, professionnelles, religieuses)
G = nx.Graph()
```

**Métriques utilisées** :
- **Degree Centrality** : Importance du nœud (nombre de voisins)
- **Betweenness Centrality** : Rôle de pont/intermédiaire
- **Clustering Coefficient** : Tendance à former des triangles (cliques)
- **Connected Components** : Identification de sous-groupes isolés
- **Community Detection** : Algorithmes de partitionnement pour dégager des pôles

#### **2. Visualisation Réseau**
```python
# Layouts exploratoires
- Spring Layout (Force-directed) : Représente les forces d'attraction/répulsion
- Circular Layout : Organisation par pôles administratifs radiaux
- "Cosmogonie" : Disposition planétaire autour de pôles centraux
```

**Paramètres visuels** :
- **Taille des nœuds** ∝ Degree (importance dans le réseau)
- **Couleurs** : Codage par institution ou époque
- **Épaisseur des arêtes** : Pondération des liens (si applicable)
- **Palette sombre** : Optimisation pour lisibilité des graphes denses

#### **3. Traitements Statistiques**
```python
import pandas as pd

# Agrégation par institution
aggregation = df.groupby('institution').agg({
    'sexe': lambda x: (x == 'homme').sum() / len(x) * 100,
    'logement': lambda x: (x == 'oui').sum() / len(x) * 100,
    'noble': lambda x: (x == 'oui').sum() / len(x) * 100
})
```

**Approches statistiques** :
- Analyse distributive par catégorie
- Ventilation démographique (% par groupe)
- Comparaison inter-institutions
- Identification de patterns et anomalies

#### **4. Pipeline de Données**
1. **Ingestion** : Lecture JSONL avec parsing itératif
2. **Extraction** : Dénormalisation des structures hiérarchiques imbriquées
3. **Filtrage** : Sélection par critères (sources, années, types de lien)
4. **Construction graphe** : Création de la structure réseau
5. **Calcul métriques** : Application d'algorithmes
6. **Visualisation** : Rendu des graphes et exports
7. **Agrégation statistique** : Production de tableaux synthétiques

---

## 📈 Résultats et Visualisations

### Réseaux Generés

#### **1. Réseaux Familiaux**
- `reseau_familial_individus.html` : Ensemble des liens de parenté
- `reseau_familial_individus_par_famille.html` : Groupement par lignées
- `reseau_familial_orbital.html` : Vue orbitale par pôles
- **Observation clé** : Forte concentration autour des grandes familles nobles

#### **2. Réseaux Professionnels**
- `reseau_interactif.html` : Liens de co-appartenance aux institutions
- `reseau_professionnel_interactif.html` : Réseau spécialisé par charges
- **Observation clé** : Clustering net par maison (Roi, Reine, etc.)

#### **3. Réseaux Religieux**
- `bulles_familles__religieux.html` : Liens religieux familialisés
- `reseau_interactif_religieux.html` : Réseau religieux complet
- `reseau_institutions_religieux_interactif.html` (sources) : Version sourcée
- **Observation clé** : Séparation nette chapelle du Roi / chapelle de la Reine

#### **4. Réseaux d'Institutions**
- `reseau_institutions_interactif.html` : Graphe des institutions interconnectées
- `reseau_institutions_familliales_interactif.html` : Vue mixte institutions/lignées
- **Observation clé** : Hiérarchie clairement visible, avec quelques ponts inter-maisons

#### **5. Graphes Analytiques**
- `cercle_hierarchie.html` : Représentation hiérarchique circulaire
- `institutions_stats_percentages.html` : Tableau de statistiques interactif

### Statistiques Clés

**Dataset Global** :
- **Personnes** : ~15 000+ enregistrements
- **Liens interpersonnels** : ~8 000+ relations cataloguées
- **Institutions** : 100+ entités (niveaux hiérarchiques 1-7)
- **Couverture temporelle** : Majoritairement XVIIe-XVIIIe siècle

**Profil Démographique** :
- **Genre** : Très forte masculinité (~99% dans beaucoup d'institutions)
- **Noblesse** : Disparité selon institution (0-10% nobles)
- **Logement** : Très faible proportion de personnes logées (~1-5%)

**Démographie de la Maison Royale** :
- **Gardes du corps** : 6 193 pers.
- **Garde-robe** : 897 pers. (96% hommes)
- **Écuries** : 776+ pers. (99%+ hommes)
- **Musique de la Chambre** : 439 pers. (5.92% femmes - exception notable)
- **Chambre du Roi** : 235 pers. (8% femmes)

---

## 🛠️ Technologies et Bibliothèques

### **Langage**
- **Python 3.7+**

### **Bibliothèques Principales**
```python
# Gestion données
import json
import pandas as pd
import numpy as np

# Théorie des graphes
import networkx as nx

# Visualisation
import matplotlib.pyplot as plt
import plotly.graph_objects as go  # (pour HTML interactif)

# Utilitaires
from collections import defaultdict, Counter
```

### **Outils de Visualisation**
- **NetworkX + Matplotlib** : Graphes statiques haute résolution
- **Plotly** : Graphes interactifs HTML (zoom, hover, sélection)
- **Graphviz** (optionnel) : Rendus hiérarchiques
- **D3.js** (optionnel) : Visualisations web avancées

### **Formats de Sortie**
- **HTML interactif** : Explorations visuelles exploratoires
- **CSV/TSV** : Données tabulaires pour analyse externe
- **PNG/PDF** : Exports statiques pour rapports
- **JSON** : Données structurées pour intégration

---

## 📁 Structure du Projet

```
Versailles-projet-Hackathon-donnees-prosocours/
│
├── README.md (CE FICHIER)
│
├── Données brutes/
│   ├── Prosocour_données_brutes.ipynb      # Analyses exploratoires brutes
│   ├── cercle_hierarchie.html              # Visualisation hiérarchique
│   ├── reseau_interactif.html              # Réseau complet interactif
│   ├── reseau_interactif_religieux.html    # Réseau religieux
│   ├── reseau_professionnel_interactif.html# Réseau professionnel
│   ├── bulles_familles__religieux.html     # Liens familiaux-religieux
│   └── .ipynb_checkpoints/
│
├── Données pures/
│   ├── Sources/
│   │   ├── Prosocours_sources.ipynb        # Nettoyage base sourcée
│   │   ├── institutions_stats_percentages.csv  # Tableau statistique
│   │   ├── institutions_stats_percentages.html # Tableau interactif
│   │   ├── bulles_familles__religieux_sourcé.html
│   │   ├── reseau_institutions_interactif.html
│   │   ├── reseau_institutions_familliales_interactif.html
│   │   ├── reseau_institutions_religieux_interactif.html
│   │   └── .ipynb_checkpoints/
│   │
│   └── Dates/
│       ├── reseau_familial_individus.html
│       ├── reseau_familial_individus_par_famille.html
│       ├── reseau_familial_orbital.html
│       └── .ipynb_checkpoints/
│
├── Statistiques/
│   └── institutions_stats_percentages.html
│
└── Presentation1.pdf                       # Présentation du projet
```

---

## 📊 Résultats et Conclusions

### Cohérence et Apports

✅ **Résultats Satisfaisants** :

1. **Décodage Structurel** : Les graphes révèlent clairement la hiérarchie de la cour (Maisons royales, niveaux d'emploi)

2. **Cohérence Historique** : Les pôles et clusters détectés correspondent aux connaissances thématiques :
   - Séparation nette Maison du Roi / Maison de la Reine
   - Importance des Gardes vs. services domestiques
   - Rôle minoritaire des femmes (sauf Musique et Chambre)

3. **Nouvelles Perspectives** :
   - Visualisation des **réseaux d'influence** (centralité)
   - Identification de **liens croisés** entre institutions
   - Quantification de la **démographie des pôles**

4. **Reproductibilité** : 
   - Code modulaire et documenté
   - Pipeline d'ingestion robuste
   - Exports réutilisables (CSV, JSON)

### Limitations et Perspectives

⚠️ **Limitation Actuelles** :
- Source data incomplète (certains liens non sourcés)
- Couverture temporelle partielle (XVIIe-XVIIIe siècle)
- Genre fortement déséquilibré
- Manque de contexte sur les charges éphémères

🔮 **Améliorations Futures** :
- Analyse temporelle fine (évolution par décennie/règne)
- Modèles prédictifs de statut/influence
- Intégration de données externes (généalogies, archives)
- Analyses d'ego-networks (réseaux personnels ciblés)

---

## 🙏 Remerciements

**Nous remercions chaleureusement le Centre du Château de Versailles** pour nous avoir confié cette base de données riche et complexe, pour l'accès aux documentations historiques, et pour la pertinence du défi posé.

Grâce à cette collaboration, nous avons pu démontrer comment des méthodes computationnelles modernes (théorie des graphes, analyse statistique) peuvent enrichir l'approche prosopographique traditionnelle et offrir une **compréhension nouvelle et visuelle des dynamiques sociales du Grand Siècle**.

Nous remercions également, à titre plus personnel, Monsieur Chahan V.-G pour son accompagnement et ses conseils précieux tout au long du projet. C'est une véritable chance d'avoir pu suivre le Hacktaton sous son organisation, et nous espérons que les résultats produits seront à la hauteur de ses attentes.

---

## 📝 Références Méthodologiques

### Articles et Documentation
- **NetworkX Documentation** : https://networkx.org/
- **Plotly Documentation** : https://plotly.com/python/
- **Théorie des Graphes** : "Graph Theory" de Reinhard Diestel
- **Analyse de Réseaux Sociaux** : "Social Network Analysis" de Stanley Wasserman et Katherine Faust

### Métadonnées Projet
- **Dates** : Février 2026
- **Équipe** : Martin H, Côme P, Juliette G, Julie D, Philippe C.-R.
- **Institution Partenaire** : Château de Versailles, Centre de Recherches
- **Type** : Hackathon Données / Digital Humanities / Histoire computationnelle
- **Statut** : Archivé - Résultats accessibles

---

## 📧 Contact & Support

Pour toute question ou demande de clarification sur la méthodologie :
- Consultez les notebooks commentés dans `Données brutes/` et `Données pures/`
- Vérifiez la documentation inline des fonctions Python
- Explorez les visualisations HTML (interactives et auto-explicatives)

---

**Version** : 1.0  
**Dernière mise à jour** : Février 2026  
**Licence** : [Collaboration académique]

---

### 🎯 Résumé Exécutif

Ce projet transforme une base de données prosopographique complexe en **visualisations argumentées et analyses statistiques robustes** du tissu social de la cour de Versailles. 

Par la combinaison de **théorie des graphes, statistiques descriptive et validation historique**, nous avons produit :

✨ **6+ réseaux interactifs** explorables  
✨ **1 tableau statistique** complet de 728 institutions  
✨ **Métriques multi-dimensionnelles** (centralité, clustering, communautés)  
✨ **Validation historique** conforme aux connaissances du Grand Siècle  

Les résultats démontrent une **réelle cohérence structurelle et apportent une compréhension nouvelle** des hiérarchies, influences et dynamiques relationnelles au sein de l'administration royale.
