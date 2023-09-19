# Set up and run STEMMUS-SCOPE on SURF research cloud (SRC).

This is an instruction about how to set up [SURF research cloud](https://www.surf.nl/en/surf-research-cloud-collaboration-portal-for-research) (SRC) for executing the [notebook](https://github.com/EcoExtreML/STEMMUS_SCOPE_Processing/blob/main/docs/notebooks/run_model_in_notebook.ipynb) of the STEMMUS-SCOPE model using executable file.

## For administrators

#### Access to SRC
To get access to SRC, you need to apply for the compute services via the [request portal](https://www.surf.nl/en/research-it/apply-for-access-to-compute-services). When your application is approved, SURF will send you an invitation with the login to SRC.

#### Create workspace
For system administrators who want to create workspace on SURF research cloud for configuring the environment and running the STEMMUS-SCOPE model, please check [this document](./create_workspace.md).

#### Give users access to workspace
Administrators can invite users to access the created workspace on SRC via the `SURF Research Access Management system`. To access the SURF Research Access Management system, visit [this site](https://sram.surf.nl/). The administrators can send invitations to new users following this [documentation](https://servicedesk.surf.nl/wiki/display/WIKI/Invite+colleagues+to+a+CO). Administrators should be invited with admin role.

## For users

#### Access to SRC
For users trying to access the existing workspace, first ask administrators to invite you. 

After receiving the invitation link, you can follow this [doc](./as_new_user.md) to create your account on SRC and access the workspace.

To log in to the SRC, click [here](https://portal.live.surfresearchcloud.nl/)

To access your workspace, follow this [instruction](https://servicedesk.surf.nl/wiki/display/WIKI/Log+in+to+your+workspace).

#### Setup environment
For users who want to configure the jupyter-workspace environment via conda and install `pystemmusscope` to execute the [notebook](https://github.com/EcoExtreML/STEMMUS_SCOPE_Processing/blob/main/docs/notebooks/run_model_in_notebook.ipynb), please check [this document](./setup_environment.md).
