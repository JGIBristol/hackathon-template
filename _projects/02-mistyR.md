---
number: 2
title: Misty
pis:
  - Miguel A. Ibarra-Arellano
  - Margot Chazotte

github: saezlab/mistyR:latest
---
# Description

This project aims to implement MistyR as a downstream module into the MCMICRO pipeline.

# Day one of the hackathon

## Setup
We first evaluated which parts and outputs of MISTyR wanted to implement and to which parameters should the user have access, to have a minimal viable project. We first agreed to implement MISTy as and option for the downstream analyis module.  

- **Input**:  
The implementation would take two input files: the quantification file generated from the quantification module, and the markers file (used on any run of MCMICRO).  

- **Output**:  
As a framework, MISTy allows for a large number of combinations of views, parameters and output files. In this implementation we are returning the user gains, contributions, interaction heatmap and interaction community. 

## Taks
- [x] Testing the mistyR docker container.
- [x] Figuring out how to run custom R scripts from inside the mistyR docker container.
- [x] Preparing a wrapper R script to specify (and for the time being limit) the scope of MISTy. 
- [x] Integrating the MISTyR docker container and the wrapper R script into a standalone nextflow.
- [ ] Forking labsyspharm/mcmicro and integrating MISTY-Nextflow as a part of downstream module.
- [ ] Test it on exemplar-001
- [ ] Submitting a pull request from labsyspharm/mcmicro. :happy_face:

# Day two of the hack'a ton


# Last working test 
<pre>
<code>
mcmicro_misty % nextflow run misty.nf -with-docker tanevesky/mistyr:latest
</code>
</pre>
