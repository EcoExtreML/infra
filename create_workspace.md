# Configure the workspace on SURF research cloud (SRC) for STEMMUS-SCOPE

In this guide, you will learn how to configure the workspace/environment on SURF research cloud for managing the resource and running the STEMMUS-SCOPE model in the [notebook](https://github.com/EcoExtreML/STEMMUS_SCOPE_Processing/blob/main/docs/notebooks/run_model_in_notebook.ipynb).

This guide assumes you already have access to SRC as the administrator of EcoExtreML project group.

## Create your workspace

To setup your workspace, you need to first log in to your [SRC portal](https://portal.live.surfresearchcloud.nl/) and follow the steps below:

- Create your storage (see the [documentation](https://servicedesk.surf.nl/wiki/display/WIKI/External+storage+volumes)).
  - Root disk (/) is too small to hold data like forcing, so an extra storage volume (/data/volume_2) is needed.
  - Choose a volume size of at least 250Gb
- Create a new workspace and attach your storage to it (see the [documentation](https://servicedesk.surf.nl/wiki/display/WIKI/Start+a+simple+workspace)).
  - Select `Jupyter Notebook` as application.
  - There are multiple pre-defiend set of virtual machines/working environments (which are called [<strong><em>flavours</em></strong>](https://servicedesk.surf.nl/wiki/display/WIKI/SRC+Available+Flavours)) available on SRC.
  - To set up the environment for STEMMUS-SCOPE, we only need to choose `SURF HPC Cloud` with preferred quantity of cpu cores and memory (e.g. 2 cpu cores and 16 GB RAM).
  - In step 5 "Options", remember to attach the storage as this is the only moment we can attach it to our workspace.
- Log in to your workspace following this [documentation](https://servicedesk.surf.nl/wiki/display/WIKI/Log+in+to+your+workspace)).

After login, you will find a notebook listed in the files named `KERNEL-README.ipynb`, which shows how to use the pre-installed `miniconda` environment on SRC. To make sure that every new user that log in to this workspace can have this manual, please execute the following command:
```sh
cp ~/KERNEL-README.ipynb /etc/skel
```

## Install Matlab Runtime
To intall Matlab Runtime for all users, it is easy to use `ansible playbook`.
An example `ansible-playbook` showing how to install matlab runtime is available [here](./install_matlab_runtime.yml). Please copy it in your jupyter-workspace and run the following command to download and install matlab runtime:

```sh
ansible-playbook install_matlab_runtime.yml
```

## Download the executable file of STEMMUS-SCOPE model
The latest version of the executable file is available in the repo [`STEMMUS_SCOPE`](https://github.com/EcoExtreML/STEMMUS_SCOPE). We can clone this repo and copy it to the shared storage:
```py
cd ~
git clone https://github.com/EcoExtreML/STEMMUS_SCOPE.git
cp STEMMUS_SCOPE /data/volume_2/
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
In order to execute the notebook and run the model, we need to copy all the forcing and boundary conditions data to the storage of SRC.

If the data is stored on a server, we can simply connect the server via SSH in our jupyter-workplace and copy the data to the SRC storage. For instance, if we have our data stored on the project space of Snellius, we can open a terminal in the jupyter-workplace and type the following command to connect to the server via SSH:
```sh
sftp user@snellius.surf.nl
```

The server will ask for your password. After typing the correct password, you should be able to access the storage system on Snellius. Now you can navigate to the path of data and download the data to the storage of SRC using the following commands:

```sh
cd /path_to_data
lcd /data/volume2/forcing
get <file>
```

To download the whole folder, use this command:

```sh
get -r <folder>
```

Now the users will be able to run the STEMMUS-SCOPE model using executable files after configuring their conda environment.