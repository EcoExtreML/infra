# Set up the conda environment for STEMMUS-SCOPE

In this guide, you will learn how to configure the conda environment in your jupyter-workspace on SURF research cloud for running the STEMMUS-SCOPE model in the [notebook](https://github.com/EcoExtreML/STEMMUS_SCOPE_Processing/blob/main/docs/notebooks/run_model_in_notebook.ipynb).

This guide assumes you already have access to SRC as a user and the workspace created by the administrator of EcoExtreML project group.

In order to run STEMMUS-SCOPE on SRC, we need to configure the `conda` environment and download the executable file.

## Managing environments and kernels on this Jupyter-workspace using `conda`
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
  (When you log in to your jupyter-workspace for the first time, a notebook called `KERNEL-README.ipynb` will be created by default and it is accessbile from files panel. In this notebook, you can find the guidelines about how to manage environments and kernels on this Jupyter-workspace.)

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

## Run STEMMUS-SCOPE model using the executable file
Now we can run the STEMMUS-SCOPE model using the executable file. Open the notebook `run_model_in_notebook.ipynb` from the path `/STEMMUS_SCOPE_Processing/docs/notebooks` in your jupyter-workspace and use the `pystemmusscope` kernel.

Before executing the notebook, remember to modify the `config` file and create your work directory. If you want to put the work directory on the shared storage (`/data/volume_2/`), remember to create your own folder to avoid conflicts. Note that the executable file and all the related forcing files are stored at `/data/volume_2/`.

Note: if this message "`error while loading shared libraries`" occurs when running the notebook in your jupyter-workspace after configuring the environment properly, please execute the cell for setting the `LD_LIBRARY_PATH`.
