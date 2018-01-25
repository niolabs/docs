# nio projects

The configuration files for nio instances are called nio projects. A project contains the configurations of the blocks, nio services, communication, and the nio instance itself. The project is functionally the source code of an instance; it defines what that instance will do within a nio system. Multiple instances can use the same project.

In addition to the configuration of an instance, the project also includes the blocks and the block code of the instance. Blocks are typically included in a project directory as Git submodules.

nio-managed instances come pre-configured with our standard project template. It is configured for our cloud environment and ships with a default set of nio Blocks.

The nio [project template repository](https://github.com/niolabs/project_template) is provided as the suggested base project for your self-managed nio instances. The project can be modified and added to to suit your requirements.

We recommend using [Git](https://git-scm.com/) for project tracking and version control, more information is available in the [project template](https://github.com/niolabs/project_template).
