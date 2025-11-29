# Analyse de la Performance Financière & Prédiction de Profit (Random Forest)

## 🚀 Vue d'Ensemble du Projet

Ce projet implémente un pipeline complet de Machine Learning, de la préparation des données brutes à la modélisation prédictive et à la simulation d'impact business. L'objectif est de comprendre les facteurs clés de la rentabilité (Profit) d'une entreprise et de fournir un outil de simulation pour aider à la prise de décision stratégique.

Les étapes couvrent : le nettoyage des données financières, l'analyse exploratoire avancée (PCA, Clustering), la modélisation de régression (Random Forest), et l'analyse MLOps (importance des features et sauvegarde de modèle).

## 📊 Pipeline et Méthodologie Technique

### 1. Data Engineering & Préparation
* **Nettoyage Robuste** : Fonctions personnalisées pour nettoyer les noms de colonnes (retrait des espaces), et les colonnes numériques (suppression des symboles de devise `$`, des virgules, gestion des formats négatifs `()`, et conversion en `float`).
* **Gestion des Manquantes** : Imputation des valeurs manquantes (`NaN`) dans les colonnes **'Discounts'** et **'Profit'** par la moyenne (`mean()`).
* **Outliers** : Traitement des valeurs aberrantes par la méthode de l'**Intervalle InterQuartile (IQR)** pour "coiffer" les valeurs extrêmes et standardiser le jeu de données.
* **Feature Engineering & Sélection** :
    * Extraction de features temporelles (`Year`, `Month`, `Day`) à partir de la colonne `Date`.
    * Analyse de **Corrélation** : Suppression des variables fortement corrélées (comme `Gross_Sales`, `COGS`, `Discounts`) pour prévenir la multicolinéarité et améliorer la stabilité du modèle.

### 2. Analyse Avancée (Dimensionality & Segmentation)
* **Standardisation** : Utilisation de `StandardScaler` pour normaliser toutes les variables numériques, préparant l'entrée pour les algorithmes sensibles à l'échelle.
* **Réduction de Dimension (PCA)** : Application d'une **Analyse en Composantes Principales** pour réduire la complexité du jeu de données et visualiser la variance.
* **Clustering (K-Means)** : Segmentation des données en clusters (groupes) pour identifier des comportements commerciaux distincts, avec analyse de la moyenne des groupes (`groupby('Cluster').mean()`).

### 3. Modélisation et MLOps
* **Modèle** : Entraînement d'un **Random Forest Regressor** pour prédire le `Profit`.
* **Évaluation** : Le modèle a atteint un **R² Score de 0.9280** sur l'ensemble de test, indiquant une forte capacité prédictive (Validation croisée moyenne R²: 0.8768).
* **Importance des Features** : L'analyse d'importance confirme que **'Sale_Price'** et **'Units_Sold'** sont les facteurs les plus critiques pour la détermination du profit.
* **Sauvegarde MLOps** : Le modèle entraîné (`rf_model`) est sauvegardé au format `.pkl` pour un déploiement futur dans un pipeline de production.

### 4. Simulation Business (Valeur Ajoutée)
* **Outil de Simulation** : Implémentation d'une fonction (`simulate_profit_impact`) pour tester des scénarios hypothétiques.
* **Résultat** : La simulation permet de quantifier l'impact direct d'une variation (ex: +/- 10%) sur les features les plus importantes (comme le prix de vente) sur le profit prédit.

## 🛠️ Outils et Librairies

* **Python**
* **Pandas & NumPy** (Manipulation et calcul)
* **Matplotlib & Seaborn** (Visualisation)
* **Scikit-learn** (StandardScaler, PCA, KMeans, RandomForestRegressor, Cross-Validation)
* **Joblib** (Sauvegarde de modèle)