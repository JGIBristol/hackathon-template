---
number: 3
title: Starfish
pis:
  - Sebastian Gonzalez Tirado
  - Florian Wuennemann

github: https://github.com/spacetx/starfish
---
# Description

This project aims to implement Starfish for image based-transcriptomics processing as module into the MCMICRO pipeline.

# Day one of the hackathon 

## Setup
We first determined, which functions from starfish we want to implement during the hackathon, to have a minimal viable project. Early on, we decided not to try and implement another stitching and registration method and assume that the user inputs a stitched, registered image. We determined that we needed 3 functions:

1) Tiling
2) Converting files to spacetx format
3) Decoding of spots

We then set out, to implement these functions into the MCMICRO code.

## Testing of the starfish Docker container
Starfish does have an existing Docker container for the most recent stabled release v0.2.2, which is available from Dockerhub via docker pull spacetx/starfish:0.2.2. (https://hub.docker.com/r/spacetx/starfish/tags).


To test whether the Docker image is functional, we test run a script from Sebastian called decoding.py inside the container. This worked without problems and suggested to us, that we can use this container without problems.

## Figuring out how to run custom python scripts within nextflow
The next part that took us some time to figure out, was how we can run the python scripts that will execute the different functions within nextflow, if we can't add them to the existing starfish Docker container. We took the roadie helper script in MCMICRO as an example and determined, that we can put the scripts inside the MCMICRO github repository and call them from there.

## Modifying MCMICRO code to have a new module called iss_decoding
Since MCMICRO did not feature an iss decoding method, we added a new module called iss_decoding. As a first step, we added multiple lines to the /config/defaults.yml file. We specified that iss_decoding: false so it won't be run by default. Then we specified the method starfish inside the module iss_decoding. Currently, we only added the parameter --tile-size 2000 for option starfish. Next, we created a new nextflow file in /modules called iss_decoding. In this file, we added a process called decode and a workflow called starfish. Based on artems template, we modified these files to run our custom python script for decoding. As a first test, we only ran it with data that is shipped with starfish, so we simply loaded the data within the python script and then procesed it, without getting any output files.

## Adding start-at and stop-at options and final test
One of the things that took us the longest to figure out, was how to tell MCMICRO to only run our new process and nothing else like registration or segmentation. We finally figured out, that we needed to add our iss_decoding module to a file in /lib/mcmicro/Flow.groovy for it to be able to call it in start-at and stop-at. Once we had added it in the right places in the Flow.groovy file, we were able to run only our iss_decoding module.

## Final test of the day
Finally, our goal of the day was to make one custom process work in MCMICRO, even if it didnt use any input or output data. We thus again, ran our decoding.py script but this time from within a process and a workflow inside MCMICRO. Our tests succeded, and we were able to run the script using the following command with the following /yml file:

<pre>
<code>nextflow run main.nf --params ./starfish/test_iss_decoding.yml --in ../exemplar-001 -resume
## Contents of test_iss_decoding.yml
workflow:
  start-at: iss_decoding
  stop-at: iss_decoding
  iss_decoding: true
</code>
</pre>