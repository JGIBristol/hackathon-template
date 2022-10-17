---
title: How to add a new module to MCMICRO
menu_title: Instructions
menu_icon: book
---

On this page, you will find information to help guide you through adding a new module to MCMICRO. There are two major situations that you can face when wanting to add a module. Some steps are common for both situations and so we will list them before going into details. No matter which section applies to you, here is what you should start with at the beginning of the hackathon:

# Requirements

- Nextflow installed
- Git installed
- Docker container for your method (publicly exposed online)


# General steps

- Fork MCMICRO master from : https://github.com/labsyspharm/mcmicro
- Make a branch for your new module:
<pre>
<code>git checkout -b [your_module_name] </code>
</pre>

Now you are ready to make changes to your branch to add your module and test it using nextflow.
Choose from the two options below that fits your case:

# 1) Adding a module for an existing section (example: segmentation)
Let's say you want to add a new module for segmentation. This is generally a bit easier, since most of the nextflow code for using the method already exists. All you have to do is to add information about the container and the command used here: [MCMICRO defaults.yml](https://github.com/labsyspharm/mcmicro/blob/5e56a0af5bde81cf3884a26ae1bdaf8745f9fb70/config/defaults.yml#L33-L70).



# 2) Adding a module for a new section of a workflow
The other, slightly more difficult situation is if you have a tool that does something that is not implemented in the MCMICRO workflow yet, for example processing of ISS data using starfish. In this case, you will have to slightly more lines of code and modify some nextflow lines in the MCMICRO repository