# Analyse du marché Airbnb à New York (2024)

> Étude exploratoire du marché de la location courte durée à New York, réalisée pour identifier les opportunités d'investissement immobilier les plus pertinentes.

---

## Contexte

Ce projet a été mené dans le cadre d'une mission fictive pour un **fonds d'investissement immobilier** souhaitant se positionner sur le marché de la location courte durée à New York. L'objectif est d'apporter une lecture data-driven du marché afin d'orienter la stratégie d'acquisition.

**Questions clés :**

- Quels quartiers offrent le meilleur potentiel de rentabilité ?
- Quels types de biens (entire home, private room…) sont les plus rentables ?
- Quel positionnement prix adopter selon la zone ciblée ?
- Le marché est-il dominé par des particuliers ou des professionnels ?

---

## Données

- **Source :** [New York Airbnb Open Data 2024 — Kaggle](https://www.kaggle.com/datasets/vrindakallu/new-york-dataset)
- **Volume initial :** 20 758 annonces × 22 variables
- **Volume après nettoyage :** 20 550 annonces (99,1 % conservé) × 25 variables
- **Variables clés :** prix, quartier, type de logement, nombre d'avis, disponibilité, nombre de chambres, hôte…

> Les fichiers de données ne sont pas versionnés (voir `.gitignore`). Le CSV brut est téléchargeable directement depuis Kaggle.

---

## Structure du projet

```text
projet-airbnb-nyc/
├── data/
│   ├── raw/                  # Dataset brut (Kaggle) — non versionné
│   └── processed/            # Dataset nettoyé et enrichi — non versionné
├── notebooks/
│   └── analyse_airbnb.ipynb  # Notebook principal d'analyse
├── outputs/
│   └── figures/              # Visualisations exportées
├── presentation/
│   └── Analyse_Airbnb_NYC.pptx  # Livrable final
├── requirements.txt          # Dépendances Python
├── .gitignore
└── README.md
```

---

## Démarche

Le notebook suit une démarche d'analyse en plusieurs étapes :

### 1. Sourcing et exploration

Chargement du dataset, analyse des types de données, statistiques descriptives et identification des valeurs manquantes.

### 2. Nettoyage

- Conversion des colonnes mal typées (`rating`, `bedrooms`, `baths`) en numérique
- Gestion des valeurs textuelles (`"No rating"`, `"Studio"`, `"Not specified"`)
- Suppression des outliers selon des seuils métier justifiés :
  - Prix entre 10 et 1 000 $/nuit
  - Minimum de nuits ≤ 365
  - Nombre de lits ≤ 10, salles de bain ≤ 6

### 3. Feature engineering

Création de variables à forte valeur analytique :

- `revenu_estime` — revenu mensuel estimé (`price × reviews_per_month`)
- `categorie_prix` — segmentation Low-cost / Standard / Luxe
- `type_hote` — Particulier / Multi-propriétaire / Professionnel

### 4. Analyse et visualisation

- Carte des prix par quartier
- Top quartiers les plus rentables
- Comparaison des types de logement
- Croisement quartiers × catégories de prix

---

## Installation et utilisation

### Prérequis

- Python 3.10 ou supérieur
- Git

### Mise en place

```bash
# Cloner le dépôt
git clone https://github.com/Manonsigilla/Airbnb-immo-analysis.git
cd Airbnb-immo-analysis

# Créer un environnement virtuel (recommandé)
python -m venv venv
venv\Scripts\activate           # Windows
source venv/bin/activate        # Mac/Linux

# Installer les dépendances
pip install -r requirements.txt

# Télécharger le dataset depuis Kaggle et le placer dans :
#   data/raw/new_york_listings_2024.csv

# Lancer Jupyter
jupyter notebook notebooks/analyse_airbnb.ipynb
```

---

## Stack technique

| Outil                    | Usage                                 |
| ------------------------ | ------------------------------------- |
| **pandas**               | Manipulation et nettoyage des données |
| **numpy**                | Calculs numériques                    |
| **matplotlib / seaborn** | Visualisations                        |
| **Jupyter Notebook**     | Environnement d'analyse               |

---

## Livrables

- **Notebook complet** : [`notebooks/analyse_airbnb.ipynb`](notebooks/analyse_airbnb.ipynb)
- **Visualisations** : [`outputs/figures/`](outputs/figures/)
- **Présentation finale** : [`presentation/Analyse_Airbnb_NYC.pptx`](presentation/Analyse_Airbnb_NYC.pptx)

---

## Auteure

**Manon Sigaud**
Projet réalisé dans le cadre d'une formation Data Analyst.
