# Configure the workspace on SURF research cloud (SRC) for STEMMUS-SCOPE

In this guide, you will learn how to configure the workspace/environment on SURF research cloud for managing the resource and running the STEMMUS-SCOPE model in the [notebook](https://github.com/EcoExtreML/STEMMUS_SCOPE_Processing/blob/main/docs/notebooks/run_model_in_notebook.ipynb).

This guide assumes you already have access to SRC as the administrator of EcoExtreML project group.

## Create your workspace

To setup your workspace, you need to first log in to your [SRC portal](https://portal.live.surfresearchcloud.nl/) and follow the steps below:

- Create your storage (see the [documentation](https://servicedesk.surf.nl/wiki/display/WIKI/External+storage+volumes)).
- Create a new workspace and attach your storage to it (see the [documentation](https://servicedesk.surf.nl/wiki/display/WIKI/Start+a+simple+workspace)).
  - There are multiple pre-defiend set of virtual machines/working environments (which are called [<strong><em>flavours</em></strong>](https://servicedesk.surf.nl/wiki/display/WIKI/SRC+Available+Flavours)) available on SRC.
  - To set up the environment for STEMMUS-SCOPE, we only need to choose `SURF HPC Cloud` and `jupyter-workspace` environment with preferred quantity of cpu cores and memory.
  - In step 5 "Options", remember to attach the storage as this is the only moment we can attach it to our workspace.
- Log in to your workspace follwing this [documentation](https://servicedesk.surf.nl/wiki/display/WIKI/Log+in+to+your+workspace)).

## Install Matlab Runtime
To intall Matlab Runtime for all users, we must use `ansible playbook`.
An example `ansible-playbook` showing how to install matlab runtime is available [here](./matlab_runtime.yml). Please copy this notebook in your jupyter-workspace and run the following command to download and install matlab runtime:

```sh
ansible-playbook matlab_runtime.yml
```

## Download the executable file of STEMMUS-SCOPE model
The latest version of the executable file is available in the repo [`STEMMUS_SCOPE`](https://github.com/EcoExtreML/STEMMUS_SCOPE). We can clone this repo and copy the executable file to the shared storage:
```py
cd ~
git clone https://github.com/EcoExtreML/STEMMUS_SCOPE.git
cp STEMMUS_SCOPE/run_model_on_snellius/exe/STEMMUS_SCOPE ~/data/volume_2/
```

Note: currently `STEMMUS_SCOPE` is a private repo and therefore it is not allowed to clone it using `HTTPS`. We have to setup `SSH` connection for it.

To generate a new ssh key, run the following command in your terminal:
```sh
ssh-keygen -t ed25519 -C "your_email@example.com"
```
Ensure the ssh-agent is running by checking:
```sh
eval "$(ssh-agent -s)"
```
If we can see `Agent pid xxxxx`, then you can add your SSH private key to the ssh-agent:
```sh
ssh-add ~/.ssh/id_ed25519
```

And finally you can add your public key to the github in `settings/SSH and GPG keys`.

(For more details about generating ssh key and adding it to github, check this [documentation](https://docs.github.com/en/authentication/connecting-to-github-with-ssh/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent)).

## Copy forcing data to the shared storage

Now the users will be able to run the STEMMUS-SCOPE model using executable files after configuring their conda environment.