# Azure DevOps Crypto Bill of Materials (CBOM) Generation Pipeline

## Overview

This repository contains an Azure DevOps (ADO) pipeline configuration for generating Crypto Bill of Materials (CBOM) for Python applications using cbomkit_theia. The pipeline automates the process of analyzing cryptographic assets and generating detailed inventories.

## 🔒 CBOM Generation Pipeline

### Purpose
The CBOM pipeline generates a comprehensive inventory of cryptographic assets within Python applications, providing transparency into the cryptographic components and their configurations.

### Key Features
- Multi-stage Docker build process for Python applications
- Automated CBOM generation using cbomkit_theia
- CycloneDX-format output
- Seamless integration with Azure DevOps
- Artifact publication for easy access

## Project Structure

```
cbom/
├── Dockerfile              # Multi-stage Docker build configuration
├── main.py                # Application entry point
├── src/
│   └── appy/             # Main application package
│       ├── core/         # Core application logic
│       ├── utils/        # Utility functions
│       └── assets/       # Application assets
└── azure-pipelines.yml   # ADO pipeline configuration
```

## Application Components

### Core Application
The Python application includes:
- Image to ASCII conversion functionality
- HTTP requests for external API integration
- File system operations
- Modular architecture with separate utils and core components

### Docker Configuration
The Dockerfile implements a multi-stage build:

1. **Build Stage**
   ```dockerfile
   FROM python:3.9.0-slim as build
   # Build wheel package
   # Validate wheel contents
   ```

2. **App Stage**
   ```dockerfile
   FROM python:3.9.0-slim as app
   # Security: Non-root user setup
   # Application installation
   # Runtime configuration
   ```

Key Features:
- Python 3.9.0 base image
- Non-root user execution
- Multi-stage build for smaller final image
- Wheel package validation
- Configurable build arguments

## Pipeline Structure

The Azure DevOps pipeline consists of four main stages:

1. **Docker Image Pull**
   ```yaml
   - script: |
       docker pull nihharika/cbomkit_theia:latest
   ```

2. **Application Build**
   ```yaml
   - script: |
       podman build -t my-python-app .
   ```

3. **CBOM Generation**
   ```yaml
   - script: |
       podman save my-python-app > my-app.tar
       podman run --rm -v $(pwd):/data nihharika/cbomkit_theia:latest image get /data/my-app.tar > enriched_CBOM.json
   ```

4. **Results Publication**
   ```yaml
   - task: PublishBuildArtifacts@1
     inputs:
       pathToPublish: "enriched_CBOM.json"
       artifactName: "CBOM"
   ```

## Generated CBOM Insights

The CBOM provides detailed information about:
- Cryptographic certificates
- Certificate details:
  - Subject and Issuer names
  - Validity periods
  - Signature algorithms
  - Public key information
- Cryptographic dependencies
- Security configurations

## Prerequisites

- Azure DevOps environment
- Docker/Podman installation
- Python project to analyze
- Access to cbomkit_theia Docker image
- Internet access for pulling dependencies

## Getting Started

1. Clone this repository
2. Ensure your Python project follows the required structure
3. Configure the pipeline in Azure DevOps:
   ```yaml
   trigger:
     - main

   pool:
     vmImage: ubuntu-latest
   ```
4. Run the pipeline

## Tools Used

- **cbomkit_theia**: CBOM generation tool
- **Docker/Podman**: Container runtime
- **Azure DevOps**: CI/CD platform
- **Python**: Application runtime
- **CycloneDX**: CBOM format specification

## Security Benefits

- Complete cryptographic asset visibility
- Enhanced security assessment capabilities
- Compliance documentation support
- Supply chain security improvement
- Risk assessment facilitation

## Contributing

1. Fork the repository
2. Create a feature branch
3. Submit a pull request

## License

[Insert your license information here]

---

For more information about cbomkit_theia, visit [cbomkit Documentation]