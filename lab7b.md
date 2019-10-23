# Lab Exercise 7b: Community Diversity in the Early Devonian New Scotland Formation (samples collected on our field trip). 

## Instructions

Complete the following lab exercise and submit your answers as Word, Pages, or PDF document and your R script as a .r file by the start of lab on October 31, 2019 (:ghost: :jack_o_lantern: :skull:). Please submit your files by email to noel.heim@tufts.edu.

## Objectives
The purpose of this lab is to learn about biodiversity by measuring it in the samples we collected from the New Scotland formation earlier this month.

## Introduction
The New Scotland Formation is Early Devonian in age, belongs to the Helderberg Group, and is exposed in eastern New York. (See the figure below)

![strat column](lab7bFigs/StratColumn.png)
*Genarliaed stratigraphic column of the Lower Devonian (and Late Silurian) Helderberg Group in Eastern New York. Our samples came from the New Scotland Formation. (Wilson 2014* Field Guide to the Devonian Fossils of New York*).*

There are a variety of ways to think about diversity. The simplest, and most common, is to think of diversity simply as the number of species (or genera, families, etc.). This metric is called **species richness** or just **richness** (S). This is the main metric we will use in this lab.

It is interesting to know how many species there are in a sample, bed, formation, etc. If we have this information, we can then make comparisons (perhaps using [rarefaction](https://github.com/naheim/rTutorials/blob/master/rarefaction.md) or some other sample standardization) between samples, formation, etc. However, we might also want to know how diversity changes through space or time. We can do this by taking a hierarchical approach to measuring biodiversity. 

Modern ecologists often consider the diversity at multiple levels. Alpha diversity (&alpha;) is defined as the diversity (simple richness or some other diversity measure) of a local sample taken from a homogeneous habitat, gamma diversity (&gamma;) is the diversity of a regional sample that includes multiple habitats, and beta diversity (&beta;) describes how diversity increases from the &alpha; level to the &gamma; level as samples are pooled. For example the number of ant species (:ant:) on Tuft's Academic Quad is a measure of &alpha; and &gamma; would be the total number of ant species in all of Middlesex County. Beta diversity, then is the diversity gained by pooling all of the local habitats in Middlesex County.

It must be true that &alpha; <= &gamma;. The diversity that is added by summing many local habitats to arrive at &gamma; is called turnover diversity or beta diversity (&beta;). In essence, beta diversity tells us how different local habitats are from each other. If local habitats are nearly identical in their species composition, &beta; will be low. If local habitats are all very different from each other, then &beta; will be very high. 

In the geological record, we can apply this model of hierarchical diversity to samples collected in the fossil record. If you recall, we sampled six beds from the outcrop, and took three (or sometimes four) samples from each bed. With this hierarchical sampling protocol, we can partition diversity into sample diversity, beta diversity within beds and beta diversity among beds. This is called **additive diversity partitioning**.

Below is an example of additive diversity partitioning for brachiopod communities from the Carboniferous of the southern Ozark Mountains. The same sampling protocol for the Ozark study was used as our study of the New Scotland Formation: multiple samples collected within beds and multiple beds collected within the two ages. 

![Heim 2009 Fig 4](lab7bFigs/Heim09Fig4.png)

We are going to calculate the additive diversity partitioning for our field samples. The general equation is &gamma; = &alpha; + &beta;<sub>1</sub> + &beta;<sub>2</sub>. Where

* &alpha; = mean S of all samples
* &beta;<sub>1</sub> = mean beta diversity within beds
* &beta;<sub>2</sub> = beta diversity among beds

In each instance of &beta;, it is calculated as the total diversity of the level minus the average of samples within the level. In our case, &beta;<sub>2</sub> is the difference between total richness and the mean diversity of the six beds. To calculate &beta;<sub>1</sub>, first calculate the &beta; diversity for each bed as the total bed diversity minus the average diversity of the three samples within the bed. &beta;<sub>1</sub> is then the average &beta; of all six sampled beds.

Calculate &alpha;, &beta;<sub>1</sub>, and &beta;<sub>2</sub> for the New Scotland data and suing S and the measure of diversity.

#### Exercise Questions 1
Search for 'Hindsville' in the search bar at the upper right. This will take you to the summary page for the units named Hindsville.

1. 


## Evenness












