# pot_test_modelling_simul_2025

Test de d'évaluation de test sur des cuves d'électrolyse sur la base de données simulées
générées par Copilot.

## Données Type

![](simulation_modèles_eval_effets_files/figure-html\visualisation_data_with_variability-1.png){fig-align="left"}

## Modèle

La formule du **modèle linéaire mixte** à utiliser est :

``` r
model_lmer_avec_inter <- lme4::lmer(rf ~ period*group + (1 | tank) + (1| date), data = data_model)
```

Le terme d'interaction entre `period` et `group` donne l'effet de l'intervention sur le
groupe traité par rapport au groupe témoin. Le terme `(1 | tank)` indique que les cuves
sont considérées comme des effets aléatoires, permettant de capturer la variabilité entre
les cuves. Le terme `(1 | date)` permet de prendre en compte la variabilité temporelle.