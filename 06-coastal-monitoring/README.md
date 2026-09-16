# Suivi côtier et machine learning

**Jour 2 - GGOSSS 2026**

Instructeurs: Frédéric Bonou, Nourdi Njutapvoui

## Contenu de la session

Cette session couvre le suivi des processus côtiers, les indicateurs de vulnérabilité climatique et un workflow léger de machine learning pour les dynamiques côtières. Les TP utilisent des jeux de données préparés sur PAK/Kribi et le littoral camerounais afin que les participants puissent travailler pendant l'école sans manipuler de fichiers lourds.

Les TP sont conçus comme des exercices d'aide à la décision. Le notebook de dynamique côtière demande aux participants de classer les priorités de suivi à partir de cinq facteurs: Shoreline, Surface Water Velocity, Tide, Wave et Wind. Le notebook de machine learning compare six algorithmes tout en discutant le risque de leakage et l'effet de la validation spatiale.

## Organisation

| Dossier | Description |
|---|---|
| `notebooks/` | Notebooks de TP et scripts de test rapide pour la dynamique côtière, la cartographie et le machine learning. |
| `data/` | Petits jeux de données CSV utilisés par les exercices. |

## Notebooks et scripts

Ordre recommandé:

1. `notebooks/GGOSSS2026_Coastal_Dynamics_PAK_Practical.ipynb`
2. `notebooks/GGOSSS2026_ML_Coastal_Vulnerability_BD_Practical.ipynb`
3. `notebooks/GGOSSS2026_Cartographie_Resultats_Spatiaux.ipynb`
4. Scripts optionnels de vérification:
   - `notebooks/smoke_test_pak_coastal_dynamics.py`
   - `notebooks/smoke_test_bd_vulnerability_ml.py`

Les tests rapides peuvent être lancés depuis ce dossier:

```bash
python notebooks/smoke_test_pak_coastal_dynamics.py
python notebooks/smoke_test_bd_vulnerability_ml.py
```

La sortie ML attendue contient trois sections: validation aléatoire avec tous les prédicteurs, sensibilité au leakage après retrait des indices dérivés, et validation spatiale avec le jeu de prédicteurs réduit. Les scores peuvent varier légèrement selon la plateforme, mais les six modèles doivent tourner:

```text
random_validation_all_predictors
ANN_MLP accuracy ...
...

leakage_sensitivity_f1_drop
...

spatial_validation_reduced_predictors
...
```

La sortie PAK attendue contient le nombre de transects en érosion/stabilité/accrétion et le secteur prioritaire selon trois scénarios de pondération.

## Données

Les notebooks utilisent ces petits fichiers locaux:

- `data/cameroon_coastal_vulnerability_ml.csv`
- `data/cameroon_coastal_vulnerability_ml_sample.csv`
- `data/pak_shoreline_change_rates_2026.csv`
- `data/pak_coastsat_box_inventory.csv`
- `data/pak_coastsat_transect_inventory.csv`
- `data/pak_wind_zonal_stats.csv`
- `data/pak_current_points_stats.csv`
- `data/pak_integrated_coastal_factors.csv`
- `data/pak_priorites_decision_suivi.csv`
- `data/pak_typologie_processus_workshop_par_zone.csv`
- `data/selected_localities_for_maps.csv`
- `data/cameroon_ml_predictions_spatiales.csv`
- `data/cameroon_ml_predictions_spatiales_sample.csv`

Les slides, handouts, cartes interactives HTML et gros fichiers de référence sont distribués séparément, conformément aux consignes du dépôt GGOSSS. Le notebook cartographique utilise Cartopy/Natural Earth pour les cartes statiques; un premier lancement peut nécessiter Internet si les couches Natural Earth ne sont pas encore en cache.

## Avant la session

Les participants doivent créer l'environnement commun GGOSSS 2026 avant la séance:

```bash
conda env create -f environment.yml
conda activate ggosss2026
jupyter lab
```

Le TP utilise les packages déjà listés dans l'environnement du dépôt: `numpy`, `pandas`, `matplotlib`, `scikit-learn`, `cartopy`, `pyproj` et `jupyterlab`.

## Lancer les notebooks

Depuis la racine du dépôt:

```bash
cd 06-coastal-monitoring
conda activate ggosss2026
jupyter lab
```

Les notebooks utilisent uniquement des chemins relatifs.

## Figures pedagogiques

La figure de typologie par zone est reproductible a partir de `data/pak_typologie_processus_workshop_par_zone.csv` dans le notebook cartographique. Elle reprend le style des figures AHP/CVI existantes, mais elle n'est pas un nouveau calcul AHP/CVI: elle synthetise les cinq facteurs du TP PAK/Kribi.
