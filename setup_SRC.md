# Set up the environment on SURF research cloud (SRC) for STEMMUS-SCOPE

In this guide, you will learn how to set up the environment on SURF research cloud for managing the resource and running the STEMMUS-SCOPE model in the [notebook](https://github.com/EcoExtreML/STEMMUS_SCOPE_Processing/blob/main/docs/notebooks/run_model_in_notebook.ipynb).

This guide assumes you already have access to SRC as the administrator of EcoExtreML project group.

## Create your workspace

To setup your workspace, you need to first log in to your [SRC portal](https://portal.live.surfresearchcloud.nl/) and follow the steps below:

- Create your storage (see the [documentation](https://servicedesk.surf.nl/wiki/display/WIKI/External+storage+volumes)).
- Create a new workspace and attach your storage to it (see the [documentation](https://servicedesk.surf.nl/wiki/display/WIKI/Start+a+simple+workspace)).
  - There are multiple pre-defiend set of virtual machines/working environments (which are called [<strong><em>flavours</em></strong>](https://servicedesk.surf.nl/wiki/display/WIKI/SRC+Available+Flavours)) available on SRC.
  - To set up the environment for STEMMUS-SCOPE, we only need to choose `SURF HPC Cloud` and `jupyter-workspace` environment with preferred quantity of cpu cores and memory.
  - In step 5 "Options", remember to attach the storage as this is the only moment we can attach it to our workspace.
- Log in to your workspace follwing this [documentation](https://servicedesk.surf.nl/wiki/display/WIKI/Log+in+to+your+workspace)).

## Configure the environment for running STEMMUS-SCOPE

In order to run STEMMUS-SCOPE on SRC, we need to configure the `conda` environment and install [`matlab runtime`](https://nl.mathworks.com/products/compiler/matlab-runtime.html).

### Managing environments and kernels on this Jupyter-workspace using `conda`
In our jupyter-workspace, `miniconda` is pre-installed at the location `/etc/miniconda`. We will use it to create virtual python environments and install [`pystemmusscope`](https://github.com/EcoExtreML/STEMMUS_SCOPE_Processing).

To set up the `conda` environment:

- Start a "Terminal" tab in the Jupyter Lab launcher and type:
  ```py
  /etc/miniconda/bin/conda init
  ```
- Close the terminal tab and start a new one. You will see that the terminal prompt has changed to something like:
  ```py
  (base) metheuser@mywsp:
  ```
  (When you log in to your jupyter-workspace for the first time, a notebook called "KERNEL-README.ipynb" will be created by default and it is accessbile from files panel. In this notebook, you can find the guidelines about how to manage environments and kernels on this Jupyter-workspace.)

- Since this `miniconda` tool is shared by all the users on this jupyter-workspace, you should not use/modify this `base` environment. Instead, you can create and activate another pystemmusscope conda environment using the [`environment.yml`](https://github.com/EcoExtreML/STEMMUS_SCOPE_Processing/blob/main/environment.yml) file. Let's first clone the [`STEMMUS_SCOPE_Processing`](https://github.com/EcoExtreML/STEMMUS_SCOPE_Processing) repo to our workspace using `HTTPS` (not via `SSH`, otherwise you need to configure your ssh key):
  ```py
  git clone https://github.com/EcoExtreML/STEMMUS_SCOPE_Processing.git
  ```
- Now we can create the pystemmusscope conda environment using the `environment.yml` file:
  ```py
  cd STEMMUS_SCOPE_Processing
  conda env create -f environment.yml
  ```
- When the installation process is finished, we can acvtivate the pystemmusscope conda environment:
  ```py
  conda activate pystemmusscope
  ```
- Then we can create a kernel from it (make sure that the modified conda-environment is still the active one):
  ```py
  python3 -m ipykernel install --user --name pystemmusscope --display-name "pystemmusscope"
  ```



