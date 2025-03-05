# Azure DevOps Bill of Materials (BOM) Generation Pipelines

## Overview

This repository contains Azure DevOps (ADO) pipeline configurations for generating two types of Bill of Materials (BOM):
- Crypto Bill of Materials (CBOM)
- Mobile Bill of Materials (MBOM)

These pipelines are designed to enhance software security and transparency by providing detailed inventories of cryptographic assets and mobile application components.

## 🔒 Crypto Bill of Materials (CBOM) Pipeline

### Purpose
The CBOM pipeline generates a comprehensive inventory of cryptographic assets within a software project using `cbomkit_theia`.

### Key Features
- Builds Python applications as Podman/Docker images
- Generates CycloneDX-format Crypto Bill of Materials
- Publishes CBOM as an artifact in Azure DevOps

### Workflow
1. Pull cbomkit Docker image
2. Build Python application as Podman image
3. Save project as tar file
4. Generate CBOM using cbomkit
5. Publish CBOM as an ADO artifact

### Sample CBOM Insights
The generated CBOM includes:
- Cryptographic certificates
- Certificate details:
  - Subject and Issuer names
  - Validity periods
  - Signature algorithms
  - Public key information

## 📱 Mobile Bill of Materials (MBOM) Pipeline

### Purpose
The MBOM pipeline analyzes Android (.apk) applications to generate a Software Bill of Materials using Syft.

### Key Features
- Analyzes mobile application packages
- Generates detailed SBOM in JSON format
- Publishes SBOM as an artifact in Azure DevOps

### Workflow
1. Install Syft tool
2. Generate SBOM for .apk file
3. Verify SBOM generation
4. Publish SBOM as an artifact

### Sample MBOM Insights
The generated MBOM provides:
- Artifact source details
- Package metadata
- Comprehensive cataloger information
- Supported package and binary types

## Prerequisites

### For CBOM Pipeline
- Docker
- Podman
- Python project
- cbomkit_theia Docker image

### For MBOM Pipeline
- Syft
- .apk file to analyze

## Getting Started

1. Clone this repository
2. Configure your Azure DevOps pipeline
3. Customize the pipeline YAML files for your specific project
4. Ensure all prerequisites are met

## Tools Used
- cbomkit_theia
- Syft
- Azure DevOps
- Docker/Podman
- CycloneDX

## Security Benefits
- Comprehensive asset inventory
- Cryptographic asset tracking
- Transparency in software composition
- Enhanced supply chain security
