# hashiconf-2026-supplemental

Supplemental material for **TLK 1335: Beyond the Laptop: Scaling Secure Dev Environments with
Nomad and Consul Mesh**, a talk on Remote Development Workspaces (RDW) at IBM HashiConf 2026
(Atlanta, GA, October 26–29).

Developer machines, and the AI agents running on them, hold source code, credentials, public
registry access, open egress, and sometimes a path to production. Remote Development Workspaces
moves that work off the laptop and onto a HashiStack platform: each workspace runs as a Nomad job
inside a Consul service mesh, built from trusted, digest-pinned images, with egress, package
sources, and git access going through the platform.

- Slides: [TLK 1335 Beyond the Laptop-1.pdf](TLK%201335%20Beyond%20the%20Laptop-1.pdf)
- Website: <https://infrashift.io>

## HashiStack Ansible collection

[infrashift/ansible-collection-infrashift-hashistack-2](https://github.com/infrashift/ansible-collection-infrashift-hashistack-2):
an Ansible collection that automates a HashiStack (Nomad, Consul, Vault) datacenter. It also
contains the Terraform live roots and demos behind Remote Development Workspaces.

## Related InfraShift repositories

### Collection lineage and dependencies

| Repository | Description |
|---|---|
| [ansible-collection-infrashift-hashistack](https://github.com/infrashift/ansible-collection-infrashift-hashistack) | Original home of the collection, superseded by `ansible-collection-infrashift-hashistack-2` |
| [ansible-role-nomad-provisioner](https://github.com/infrashift/ansible-role-nomad-provisioner) | Ansible role that provisions HashiCorp Nomad; listed in the collection's `requirements.yml` |

### Trusted images and devcontainer supply chain

| Repository | Description |
|---|---|
| [trusted-base-images](https://github.com/infrashift/trusted-base-images) | Trusted base OCI images built on Red Hat UBI9 and UBI10; the digest-pinned base for every devcontainer |
| [trusted-service-containers](https://github.com/infrashift/trusted-service-containers) | DHI mirrors and UBI9-micro service containers with a three-actor signing chain and a fail-closed OPA gate; the bases for workspace companion services |
| [trusted-devcontainer-templates](https://github.com/infrashift/trusted-devcontainer-templates) | Devcontainer templates built on the trusted base images; each seed starts from one |
| [trusted-devcontainer-features](https://github.com/infrashift/trusted-devcontainer-features) | Devcontainer features for the trusted devcontainers |

### Remote development workspace seeds

A seed is the starting repository for a new workspace. Each one pairs a trusted devcontainer
template with the workspace runtime contract.

| Repository | Description |
|---|---|
| [trusted-devcontainer-seed-ansible-cue](https://github.com/infrashift/trusted-devcontainer-seed-ansible-cue) | ansible-core on Python 3.13, plus CUE |
| [trusted-devcontainer-seed-dotnet-node](https://github.com/infrashift/trusted-devcontainer-seed-dotnet-node) | .NET SDK, Node.js, npm, and pnpm |
| [trusted-devcontainer-seed-go-cue](https://github.com/infrashift/trusted-devcontainer-seed-go-cue) | Go and CUE |
| [trusted-devcontainer-seed-java](https://github.com/infrashift/trusted-devcontainer-seed-java) | OpenJDK 21, Maven, and Gradle |
| [trusted-devcontainer-seed-python](https://github.com/infrashift/trusted-devcontainer-seed-python) | Python 3.13, uv, and ruff |
| [trusted-devcontainer-seed-neovim-ansible-cue](https://github.com/infrashift/trusted-devcontainer-seed-neovim-ansible-cue) | Terminal-first: tmux and Neovim/LazyVim with Ansible and CUE (ansible-lint, CUE LSP) |
| [trusted-devcontainer-seed-neovim-go](https://github.com/infrashift/trusted-devcontainer-seed-neovim-go) | Terminal-first: tmux and Neovim/LazyVim with Go |
| [trusted-devcontainer-seed-neovim-java](https://github.com/infrashift/trusted-devcontainer-seed-neovim-java) | Terminal-first: tmux and Neovim/LazyVim with Java (jdtls) |
| [trusted-devcontainer-seed-neovim-python](https://github.com/infrashift/trusted-devcontainer-seed-neovim-python) | Terminal-first: tmux and Neovim/LazyVim with Python (basedpyright, ruff) |

### Demo companions

| Repository | Description |
|---|---|
| [chad-dotfiles](https://github.com/infrashift/chad-dotfiles) | Worked example of a portable global git configuration for a remote development workspace |

### Agent sandboxing, collaboration, and observability tools

| Repository | Description |
|---|---|
| [local-dev-workspaces-sandbox](https://github.com/infrashift/local-dev-workspaces-sandbox) | Runs an AI coding agent (Claude Code) in an isolated Fedora VM on a Linux KVM host. A zero-trust gateway (Vault, Consul, Envoy) holds every real credential, swaps the VM's surrogates for them, and enforces a default-deny egress allow list. Built with Terraform and Ansible; tested on Pop!_OS and Ubuntu 24.04. See the [security controls](https://github.com/infrashift/local-dev-workspaces-sandbox/blob/main/labs/fedora44min-x86_64-dev-ws/security-controls.md) |
| [chit](https://github.com/infrashift/chit) | Text-only chat server for humans and AI agents; used by the collection's chit-server demo. Docs: <https://infrashift.github.io/chit/> |
| [grafana-tui](https://github.com/infrashift/grafana-tui) | Lightweight, interactive terminal UI for Prometheus with Grafana dashboard support, written in Rust. Docs: <https://infrashift.github.io/grafana-tui/> |
