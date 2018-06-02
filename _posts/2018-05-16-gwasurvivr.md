---
layout: post
title: gwasurvivr
subtitle: An R/Bioconductor package for genome wide survival analyses
#gh-repo: daattali/beautiful-jekyll
#gh-badge: [star, fork, follow]
date: 2018-05-16 13:00
tags: [gwas, survival]
---
gwasurvivr 0.99.0

[gwasurvivr](https://bioconductor.org/packages/3.8/bioc/html/gwasurvivr.html)

1 Abbas Rizvi, 1 Ezgi Karaesmen, 2 Martin Morgan and 1 Lara Sucheston-Campbell

1 The Ohio State University, Columbus, OH
2 Roswell Park Comprehensive Cancer Center, Buffalo, NY

Increasingly researchers have become interested in time-to-event outcomes in the context of genetic variation. Existing software for performing survival analyses across millions of SNPs are limited. Recently, comprehensive stand-alone software packages, genipe and SurvivalGWAS_SV, were developed, however, they require user interaction with the raw output after imputation opening room for error during analysis. GWASTools, while available in R and can implement survival, is primarily for storing large SNP datasets and rigorous QC/QA. To address this unmet need, we developed an R/Bioconductor package to conduct fast and efficient genome wide survival analyses on imputed genetic data generated using IMPUTE2 and VCF data generated from Michigan or Sanger imputation servers. 

gwasurvivr implements Cox proportional hazards models to test SNP association with outcome; the package allows for covariates and SNP-covariate interaction. To potentially decrease the number of iterations needed for convergence when optimizing the parameters estimates in the Cox model,  we modified survival::coxph.fit, to fit covariates without the SNP and use those parameter estimates as initial starting points. For models without covariates the parameter estimation optimization begins with null initial value. Users can internally subset the data by providing sample IDs and pre-filter SNPs by info score and MAF. Output for each SNP includes parameter estimates, p-values, MAFs, INFO scores, number of events and total sample N. gwasurvivr is well-suited for multi-core processors and users can specify node preferences used during computation. To overcome R memory limitations gwasurvivr iteratively performs survival on subsets of the entire data.

We benchmarked our package with genipe, SurvivalGWAS_SV, and GWASTools using IMPUTE2 data for varying sample sizes (n=100, n=1000, n=5000) and SNPs (p=1000, p=10000, p=100000) including two non-genetic covariates. All packages showed excellent agreement across MAF estimates, coefficient estimates, and p-values, with gwasurvivr outperforming the other packages in time to completion for all simulations.

