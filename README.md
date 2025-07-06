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

## Points Importants

1.  **Ordonner les facteurs** dans le bon ordre pour les modèles linéaires : ref/essai et
    avant/après intervention.
2.  Utiliser des modèles linéaires avec des effets de période et de groupe **avec
    interaction**; l'**interaction période:groupe** permet de capturer l'effet du test sur
    les cuves après la date d'intervention. Les modèles sans interaction ne donnent pas le
    résultat correct. L'interprétation est que l'interaction groupe:période (cuves
    test:période test) permet d'isoler l'effet du test sur les cuves de test
    indépendamment des facteurs groupe hors période test et période hors groupe test.

## Visualisation des résultats

### Table 

```{R}
sjPlot::tab_model(model_lmer_avec_inter, 
                show.ci = FALSE, 
                digits = 3,
                show.se = TRUE, 
                show.stat = TRUE, 
                show.p = TRUE,
                pred.labels = c("(Intercept)", "Période après intervention", "Groupe test", "Interaction période: groupe test"),
                dv.labels = "Modèle linéaire hierarchique avec interaction")
```

```{R}

```