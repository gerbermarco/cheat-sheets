# Dev Containers Cheat Sheet

This cheat sheet provides a quick reference for setting up and extending Dev Container configurations.

## Table of Contents
- [Table of Contents](#table-of-contents)
- [What are Dev Containers](#what-are-dev-containers)
- [Examples](#examples)
- [Quick Links](#quick-links)
- [Snippets](#snippets)
- [Contributing](#contributing)
- [Stay updated](#stay-updated)

## What are Dev Containers

Dev Containers provide a consistent development environment using containers. The configuration is stored in `.devcontainer/devcontainer.json`, defining settings, extensions, and dependencies.

Want a more in-depth guide on Dev Containers? I've written a blog post that walks through how Dev Containers work, their benefits, and step-by-step instructions for getting started with your first Dev Container project.

Check out the blog post: [Dev Containers: Developing inside a container - marcogerber.ch](https://marcogerber.ch/dev-containers-developing-inside-a-container)

## Examples

<details>

<summary>
  <b>Simple: Using devcontainers.json</b>
  <p><i>A simple devcontainer.json example to get you going.</i></p>
</summary>

`.devcontainer/devcontainer.json`

```json
{
  "name": "simple-devcontainers-example",
  "image": "mcr.microsoft.com/devcontainers/base:ubuntu",
  "features": {
    "ghcr.io/devcontainers/features/azure-cli:1": {
      "installBicep": true
    },
    "ghcr.io/devcontainers/features/powershell:1": {
      "modules": "Az.Accounts, Az.Resources"
    },
    "ghcr.io/devcontainers/features/common-utils:2": {},
    "ghcr.io/devcontainers/features/git": {},
    "ghcr.io/devcontainers/features/python": {}
  },
  "customizations": {
    "vscode": {
      "extensions": [
        "formulahendry.auto-rename-tag",
        "ms-vscode.azurecli",
        "ms-azuretools.vscode-bicep",
        "ms-python.black-formatter",
        "sleistner.vscode-fileutils",
        "esbenp.prettier-vscode",
        "vsls-contrib.gitdoc",
        "GitHub.copilot",
        "GitHub.copilot-chat",
        "ms-toolsai.jupyter",
        "ms-python.python",
        "ms-python.vscode-pylance",
        "ms-python.debugpy",
        "oderwat.indent-rainbow",
        "wayou.vscode-todo-highlight",
        "vscode-icons-team.vscode-icons",
        "tonybaloney.vscode-pets"
      ],
      "settings": {
        "terminal.integrated.defaultProfile.linux": "bash",
        "editor.formatOnSave": true,
        "editor.defaultFormatter": "esbenp.prettier-vscode",
        "vscode-pets.petSize": "medium",
        "vscode-pets.petType": "clippy",
        "workbench.iconTheme": "vscode-icons",
        "todohighlight.keywords": [
          {
            "text": "FEATURE:",
            "color": "white",
            "backgroundColor": "#68ba7f"
          }
        ]
      }
    }
  },
  "postCreateCommand": "if [ -f \"requirements.txt\" ]; then pip install -r requirements.txt; fi && echo 'Post-creation setup complete ✅'",
  "remoteUser": "batman",
  "forwardPorts": [],
  "mounts": []
}
```

</details>

<details>

<summary>
  <b>Advanced: Using Dockerfile</b>
  <p><i>Create a Dev Container using a Dockerfile.</i></p>
</summary>

`.devcontainer/devcontainer.json`

```json
{
  "name": "advanced-devcontainers-example",
  "build": {
    "dockerfile": "Dockerfile"
  },
  "features": {
    "ghcr.io/devcontainers/features/azure-cli:1": {
      "installBicep": true
    },
    "ghcr.io/devcontainers/features/powershell:1": {
      "modules": "Az.Accounts, Az.Resources"
    },
    "ghcr.io/devcontainers/features/common-utils:2": {},
    "ghcr.io/devcontainers/features/git:1": {},
    "ghcr.io/devcontainers/features/python:1": {}
  },
  "customizations": {
    "vscode": {
      "extensions": [
        "formulahendry.auto-rename-tag",
        "ms-vscode.azurecli",
        "ms-azuretools.vscode-bicep",
        "ms-python.black-formatter",
        "sleistner.vscode-fileutils",
        "esbenp.prettier-vscode",
        "vsls-contrib.gitdoc",
        "GitHub.copilot",
        "GitHub.copilot-chat",
        "ms-toolsai.jupyter",
        "ms-python.python",
        "ms-python.vscode-pylance",
        "ms-python.debugpy",
        "oderwat.indent-rainbow",
        "wayou.vscode-todo-highlight",
        "vscode-icons-team.vscode-icons",
        "tonybaloney.vscode-pets"
      ],
      "settings": {
        "terminal.integrated.defaultProfile.linux": "bash",
        "editor.formatOnSave": true,
        "editor.defaultFormatter": "esbenp.prettier-vscode",
        "vscode-pets.petSize": "medium",
        "vscode-pets.petType": "clippy",
        "workbench.iconTheme": "vscode-icons",
        "todohighlight.keywords": [
          {
            "text": "FEATURE:",
            "color": "white",
            "backgroundColor": "#68ba7f"
          }
        ]
      }
    }
  },
  "remoteUser": "batman",
  "forwardPorts": [],
  "mounts": []
}
```

`.devcontainer/Dockerfile`

```Dockerfile
FROM mcr.microsoft.com/devcontainers/base:ubuntu
RUN apt-get update && export DEBIAN_FRONTEND=noninteractive \
    && apt-get -y install git
RUN if [ -f "requirements.txt" ]; then pip install -r requirements.txt; fi
```

</details>

More specific examples can be found in the `./examples` folder.

## Quick Links

| Type                  | Link                                                                                                                                                                                         | Examples                                                                                                                    |
| --------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------- |
| Images                | [Microsoft Container Registry Index](https://mcr.microsoft.com/v2/_catalog), [DockerHub](https://hub.docker.com/), [VS Code images](https://hub.docker.com/r/microsoft/vscode-devcontainers) | `mcr.microsoft.com/devcontainers/base:ubuntu`                                                                               |
| Properties            | [General devcontainer.json properties](https://containers.dev/implementors/json_reference/#general-properties)                                                                               | `features`                                                                                                                  |
| Properties            | [Dockerfile specific properties](https://containers.dev/implementors/json_reference/#image-specific)                                                                                         | `build.args`                                                                                                                |
| Properties            | [Lifecycle scripts](https://containers.dev/implementors/json_reference/#lifecycle-scripts)                                                                                                   | `postCreateCommand`                                                                                                         |
| Features              | [Available features](https://containers.dev/features)                                                                                                                                        | `ghcr.io/devcontainers/features/azure-cli:1": {}`                                                                           |
| Templates             | [Available templates](https://containers.dev/templates)                                                                                                                                      | `ghcr.io/devcontainers/templates/alpine:3.2.2	`                                                                             |
| Environment variables | [Env file and individual variables](https://code.visualstudio.com/remote/advancedcontainers/environment-variables)                                                                           |                                                                                                                             |
| Storage               | [Mount local disk drives](https://code.visualstudio.com/remote/advancedcontainers/add-local-file-mount)                                                                                      |                                                                                                                             |
| Storage               | [Change the default source code mount](https://code.visualstudio.com/remote/advancedcontainers/change-default-source-mount)                                                                  | `"workspaceMount": "source=${localWorkspaceFolder}/sub-folder,target=/workspace,type=bind","workspaceFolder": "/workspace"` |
| User                  | [Add a non-root user to a container](https://code.visualstudio.com/remote/advancedcontainers/add-nonroot-user)                                                                               | `"remoteUser": "batman"`                                                                                                    |
| Session               | [Persist bash history](https://code.visualstudio.com/remote/advancedcontainers/persist-bash-history)                                                                                         |                                                                                                                             |

### Official documentation

- [Development Containers documentation](https://containers.dev/)
- [Dev Containers in VS Code documentation](https://code.visualstudio.com/docs/devcontainers/containers)
  - [Advanced container configuration](https://code.visualstudio.com/remote/advancedcontainers/overview)
  - [Tips and tricks](https://code.visualstudio.com/docs/devcontainers/tips-and-tricks)
  - [Dev Containers FAQ](https://code.visualstudio.com/docs/devcontainers/faq)

## Snippets

<details>

<summary>
  <b>Install Python packages from a requirements.txt file</b>
</summary>

This installs Python packages from a `requirements.txt` file in the root folder, using the `postCreateCommand`

```json
  "postCreateCommand": "if [ -f \"requirements.txt\" ]; then pip install -r requirements.txt; fi && echo 'Post-creation setup complete ✅'",
```

</details>

<details>

<summary>
  <b>Install PowerShell modules</b>
</summary>

PowerShell modules can be declared directly with the feature.

```json
  "features": {
    "ghcr.io/devcontainers/features/powershell:1": {
      "modules": "Az.Accounts, Az.Resources"
    }
  },
```

</details>

## Contributing

Contributions to this cheat sheet are welcome! If you have additional examples, tips, or corrections:

- Submit a pull request to the repository
- Open an issue to suggest improvements
- Send a direct message with your ideas

Your contributions help make this resource more valuable for the entire community. All submissions will be reviewed promptly.

## Stay updated

For more information, tips and tricks on various Azure topics, feel free to follow my blog [marcogerber.ch](https://marcogerber.ch/).