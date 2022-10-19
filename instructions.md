---
title: How to add a new module to MCMICRO
menu_title: Instructions
menu_icon: book
---

On this page, you will find information to help guide you through adding a new module to MCMICRO. There are two major situations that you can face when wanting to add a module. Some steps are common for both situations and so we will list them before going into details. No matter which section applies to you, here is what you should start with at the beginning of the hackathon:

## Requirements

- Nextflow installed
- Git installed
- Docker container for your method (publicly exposed online)


## General steps

- Fork MCMICRO master from : https://github.com/labsyspharm/mcmicro
- Make a branch for your new module:
<pre>
<code>git checkout -b [your_module_name] </code>
</pre>

Now you are ready to make changes to your branch to add your module and test it using nextflow.
Choose from the two options below that fits your case:

## 1) Adding a module for an existing section (example: segmentation)
Let's say you want to add a new module for segmentation. This is generally a bit easier, since most of the nextflow code for using the method already exists. All you have to do is to add information about the container and the command used here: [MCMICRO defaults.yml](https://github.com/labsyspharm/mcmicro/blob/5e56a0af5bde81cf3884a26ae1bdaf8745f9fb70/config/defaults.yml#L33-L70).


## 2) Adding a module for a new section of a workflow
The other, slightly more difficult situation is if you have a tool that does something that is not implemented in the MCMICRO workflow yet, for example processing of ISS data using starfish. In this case, you will have to slightly more lines of code and modify some nextflow lines in the MCMICRO repository. 

A general template prepared by [Artem Sokolov](https://github.com/ArtemSokolov) can be found [here](https://github.com/labsyspharm/mcmicro/pull/438/files#diff-0ba9607254c8dff3f4201aa054d019f700788414c7860ff116a555c6d131c324). But we will go through this template below step by step:

<pre>
<code>Again, before any of these steps, make sure you forked the MCMICRO master branch as described above and you created a feature
branch for the module you want to add!!!</code>
</pre> 

# 2.1) Step 1: Add module specs to [config/defaults.yml](https://github.com/labsyspharm/mcmicro/blob/master/config/defaults.yml)

For example, support we wanted to add a module that produces a QC report about the signal-to-noise ratio (snr). The three additions to defaults.yml may then look as follows:
<pre>
<code>
  a: Add a flag specifying whether the module should be run to workflow:
  b: Add default module options to options:
  c: Add module name and container specs to modules:

workflow:   
    report: false 
  options:
    snr: --cool-parameter 42
  modules: 
    report:
      name: snr 
      container: myorganization/snr 
      version: 1.0.0 
</code>
</pre> 

# 2.2) Modify the following code as required and create a new file under mcmicro/modules with [your_method].nf as

<pre>
<code>
// Import utility functions from lib/mcmicro/*.groovy
import mcmicro.*

// Process name will appear in the the nextflow execution log
// While not strictly required, it's a good idea to make the 
//   process name match your tool name to avoid user confusion
process snr {

    // Use the container specification from the parameter file
    // No change to this line is required
    container "${params.contPfx}${module.container}:${module.version}"

    // Specify the project subdirectory for writing the outputs to
    // The pattern: specification must match the output: files below
    // TODO: replace report with the desired output directory
    // TODO: replace the pattern to match the output: clause below
    publishDir "${params.in}/report", mode: 'copy', pattern: "*.html"

    // Stores .command.sh and .command.log from the work directory
    //   to the project provenance
    // No change to this line is required
    publishDir "${Flow.QC(params.in, 'provenance')}", mode: 'copy', 
      pattern: '.command.{sh,log}',
      saveAs: {fn -> fn.replace('.command', "${module.name}-${task.index}")}

    // Inputs for the process
    // mcp - MCMICRO parameters (workflow, options, etc.)
    // module - module specifications (name, container, options, etc.)
    // img/sft - pairs of images and their matching spatial feature tables
  input:
    val mcp
    val module
    tuple path(img), path(sft)

    // Process outputs that should be captured and 
    //  a) returned as results
    //  b) published to the project directory
    // TODO: replace *.html with the pattern of the tool output files
  output:
    path("*.html"), emit: results

    // Provenance files -- no change is needed here
    tuple path('.command.sh'), path('.command.log')

    // Specifies whether to run the process
    // Here, we simply take the flag from the workflow parameters
    // TODO: change snr to match the true/false workflow parameter in defaults.yml
  when: mcp.workflow["report"]

    // The command to be executed inside the tool container
    // The command must write all outputs to the current working directory (.)
    // Opts.moduleOpts() will identify and return the appropriate module options
    """    
    python /app/mytool.py --image $img --features $sft ${Opts.moduleOpts(module, mcp)}
    """
}

workflow report {

    // Inputs:
    // mcp - MCMICRO parameters (workflow, options, etc.)
    // imgs - images
    // sfts - spatial feature tables
  take:
    mcp
    imgs
    sfts

  main:

    // Match images against feature tables
    id_imgs = imgs.map{ it -> tuple(Util.getImageID(it), it) }
    id_sfts = sfts.map{ it -> tuple(Util.getFileID(it, '--'), it) }

    // Apply the process to each (image, sft) pair
    id_imgs.combine(id_sfts, by:0)
        .map{ tag, img, sft -> tuple(img, sft) } | snr

    // Return the outputs produced by the tool
  emit:
    snr.out.results
}
</code>
</pre> 