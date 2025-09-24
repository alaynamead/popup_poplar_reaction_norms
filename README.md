# popup_poplar_reaction_norms
Code from "Variation in responses to temperature across admixed genotypes of Populus trichocarpa × P. balsamifera predict geographic shifts in regions where hybrids are favored"

Alayna Mead, Joie R. Beasley-Bennett, Andrew Bleich, Dylan Fischer, Shelby Flint, Julie Golightly, Sara K. Klopf, Mason W. Kulbaba, Jesse R. Lasky, Jared M. LeBoldus, David B. Lowry, Nora Mitchell, Emily Moran, Jason P. Sexton, Kelsey L. Søndreli, Baxter Worthing, Michelle Zavala-Paez, Matthew C. Fitzpatrick, Jason Holliday, Stephen Keller, Jill A. Hamilton

bioRxiv 2025.05.16.654548; doi: https://doi.org/10.1101/2025.05.16.654548 

All scripts are R markdown files.

To recreate an R environment with package versions used here, the the renv.lock file is included in the 'code' directory. See details for using the renv package [here](https://rstudio.github.io/renv/articles/renv.html).

## climate_PCA_garden_provenance_historic_future.Rmd

PCA of climate data for both provenance sites (including historic and future climates) and garden sites (yearly climates from 2020-2023).

input: data/clean/546_genotypes_provenance_future_historic_climate_with_gardens_long_format.Rda

output: Figure 1B

## transfer_function_multiyear_linear_mixed_effects_model.Rmd

Test the effects of home climate, garden climate, and genetics on the growth and mortality responses of hybrid poplars across different common gardens, then predict genotype-specific reaction norms to MCMT. Uses glmmTMB to fit a zero-inflated mixed-effects model.

input: mini_garden_phenotypic_and_climate_data_2021-2024.Rdata

output: 

* Figure 2

* Figure 4

* Figure 5

* results/model_prediction/glmTMB_multiyear_model_outputs_garden_MCMT_2021-2022_vs_GrowthIncrement_2021-2022.Rda

* results/model_prediction/predictedGrowth_acrossClimates_byGenotype_garden_MCMT_2021-2022.Rdata

## predict_maxi_garden_phenotypes.Rmd

Test whether model built from mini gardens dataset can accurately predict growth in the maxi gardens (3 sites, one of which is novel, and 544 genotypes, 500 of which are novel)

This code is mostly pulled from 'code/transfer_function_multiyear_linear_mixed_effects_model.Rmd' script

input:

* data/clean/maxi_garden_phenotypic_climate_genetic_data_2021-2023.Rdata

* results/model_prediction/glmTMB_multiyear_model_outputs_garden_MCMT_2021-2022_vs_GrowthIncrement_2021-2022.Rda

output: Figure 3

## predict_growth_future_climates.Rmd

Using the genotype-specific modeled reaction norms produced by 'transfer_function_multiyear_linear_mixed_effects_model.Rmd' script, predict how each genotype's growth and survival could change under future temperatures (represented by MCMT).

input:

* results/model_prediction/glmTMB_multiyear_model_outputs_garden_MCMT_2021-2022_vs_GrowthIncrement_2021-2022.Rda

* results/model_prediction/predictedGrowth_acrossClimates_byGenotype_garden_MCMT_2021-2022.Rdata

output: Figure S14


## map_best_genotype_by_climate.Rmd

Using reaction norms modeled in the 'transfer_function_multiyear_linear_mixed_effects_model.Rmd' script, identify the genotype having highest growth (taking into account mortality probability) across the sampled hybrid zone under historic and future values of MCMT. Maps show where the 'optimal' genotype/species ancestry could shift spatially under future temperatures, resulting in spatial shifts in the location of the hybrid zone.

input:

* results/model_prediction/predictedGrowth_acrossClimates_byGenotype_garden_MCMT_2021-2022.Rdata

* data/clean/garden_climates_average1961-1990_yearly2020-2023.Rdata

* data/clean/mini_garden_phenotypic_and_climate_data_2021-2023.Rdata

output:

* Figure 6, Figure S15

* results/model_prediction/genotypePredictedHeights_byGardenMCMT.Rdata
