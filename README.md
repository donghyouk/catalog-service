devcontainer.json
// For format details, see https://aka.ms/devcontainer.json. For config options, see the
// README at: https://github.com/devcontainers/templates/tree/main/src/java
{
  "name": "Java",
  // Or use a Dockerfile or Docker Compose file. More info: https://containers.dev/guide/dockerfile
  "image": "mcr.microsoft.com/devcontainers/java:1-21-bullseye",
  "features": {
    "ghcr.io/devcontainers/features/java:1": {},
    "ghcr.io/devcontainers/features/docker-in-docker:2": {},
    "ghcr.io/devcontainers/features/kubectl-helm-minikube:1": {},
    "ghcr.io/lentzi90/features/tilt:0": {}
  },
  // Use 'forwardPorts' to make a list of ports inside the container available locally.
  // "forwardPorts": [],
  // Use 'postCreateCommand' to run commands after the container is created.
  "postCreateCommand": "bash .devcontainer/postCreateCommand.sh",
  // Configure tool-specific properties.
  "customizations": {
    "vscode": {
      "extensions": [
        "redhat.java",
        "vmware.vscode-boot-dev-pack",
        "GitHub.vscode-github-actions",
        "redhat.fabric8-analytics"
      ]
    }
  },
  // Uncomment to connect as root instead. More info: https://aka.ms/dev-containers-non-root.
  // "remoteUser": "root"
  "mounts": [
    {
      "source": "${localEnv:HOME}/.m2",
      "target": "/home/vscode/.m2",
      "type": "bind"
    }
  ]
}
