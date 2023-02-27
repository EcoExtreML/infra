# Create the workspace on SURF research cloud (SRC) for STEMMUS-SCOPE

In this guide, you will learn how to create the workspace/environment on SURF research cloud for managing the resource and running the STEMMUS-SCOPE model in the [notebook](https://github.com/EcoExtreML/STEMMUS_SCOPE_Processing/blob/main/docs/notebooks/run_model_in_notebook.ipynb).

This guide assumes you already have access to SRC as the administrator of EcoExtreML project group.

## Create your workspace

To setup your workspace, you need to first log in to your [SRC portal](https://portal.live.surfresearchcloud.nl/) and follow the steps below:

- Create your storage (see the [documentation](https://servicedesk.surf.nl/wiki/display/WIKI/External+storage+volumes)).
- Create a new workspace and attach your storage to it (see the [documentation](https://servicedesk.surf.nl/wiki/display/WIKI/Start+a+simple+workspace)).
  - There are multiple pre-defiend set of virtual machines/working environments (which are called [<strong><em>flavours</em></strong>](https://servicedesk.surf.nl/wiki/display/WIKI/SRC+Available+Flavours)) available on SRC.
  - To set up the environment for STEMMUS-SCOPE, we only need to choose `SURF HPC Cloud` and `jupyter-workspace` environment with preferred quantity of cpu cores and memory.
  - In step 5 "Options", remember to attach the storage as this is the only moment we can attach it to our workspace.
- Log in to your workspace follwing this [documentation](https://servicedesk.surf.nl/wiki/display/WIKI/Log+in+to+your+workspace)).

## Install 