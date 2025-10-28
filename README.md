# Football-Match-Outcome-Prediction-

Ce projet personnel explore l'utilisation du **Machine Learning** pour prédire les résultats des matchs de **Premier League** (pour l'instant) (Victoire/Non-Victoire) et évaluer la rentabilité de stratégies de paris simples.

---

## Données 

Les données proviennent de [**football-data.co.uk**](https://www.football-data.co.uk/data.php) et couvrent les saisons de Premier League de **2013-2014 à aujourd'hui**. Elles incluent les résultats des matchs, les statistiques (tirs, buts, etc.) et les cotes de différents bookmakers (comme par exemple celles de **Bet365, Pinnacle**).

---

## Méthodologie 

1.  **Préparation des Données :** Transformation des données en format **"long"** (une ligne par performance d'équipe par match). Chaque match est vu du point de vue des deux équipes (il y a donc deux fois chaque match dans le tableau sortant de ma fonction prepare_data_with_form.
2.  **Feature Engineering :** Création de features basées sur la **forme récente** des équipes (moyennes glissantes sur les N derniers matchs pour les points, buts marqués/encaissés, tirs cadrés/subis). Utilisation des codes d'équipe et des cotes comme features.
3.  **Modélisation :** Utilisation d'un classifieur **XGBoost** (bien plus efficace ici qu'un random forest).
4.  **Optimisation :** Recherche des meilleurs hyperparamètres avec `GridSearchCV`, en optimisant pour différentes métriques (**`balanced_accuracy`**, **`precision`**, **`recall`**).
5.  **Évaluation :**
    * Métriques techniques : `balanced_accuracy`, `precision`, `recall`.
    * Métriques économiques : Calcul du **Retour sur Investissement (ROI)** en simulant une stratégie de pari simple ("Parier 1€ si le modèle prédit Victoire (`preds == 1`)").

---

## Résultats Clés 

* Le modèle optimisé pour la **`precision`** (hyperparamètres : `{'colsample_bytree': 0.8, 'learning_rate': 0.007, 'max_depth': 6, 'n_estimators': 60}`) a montré les meilleures performances économiques.
* Sur un jeu de test étendu (saisons 2022-2025 et début 2025-26), ce modèle a atteint un **ROI de +6.88%** sur 220 paris effectués, surpassant largement le bookmaker "suivre le favori" (ROI de -21.16%).
* L'analyse de l'importance des features montre que les **cotes des bookmakers** (surtout Pinnacle) sont dominantes, mais les **features de forme "maison"** (tirs, buts, points) apportent une valeur significative.

---

## Technologies Utilisées 

* **Python**
* **Pandas, NumPy**
* **Scikit-learn**
* **XGBoost**
* **Matplotlib, Seaborn**

---

## Prochaines Étapes 

* **Validation Robuste :** Tester le modèle profitable sur différentes périodes/saisons/championnats pour confirmer la stabilité du ROI.
* **Analyse de l'"Edge" :** Comprendre plus en détail *quels* types de paris le modèle profitable sélectionne.

---
