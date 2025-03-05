# Azure DevOps Bill of Materials (BOM) Generation Pipeline

## Overview

This repository contains an Azure DevOps (ADO) pipeline configuration for generating Mobile Bill of Materials (MBOM) for Android applications using Syft. The pipeline automates the process of analyzing APK files and generating detailed component inventories.

## 🔍 MBOM Generation Pipeline

### Purpose
The pipeline analyzes Android (.apk) applications to generate a comprehensive Software Bill of Materials, providing transparency into the application's components and dependencies.

### Key Features
- Automated MBOM generation for APK files
- JSON-formatted output with detailed package information
- Seamless integration with Azure DevOps
- Artifact publication for easy access and sharing

### Workflow
1. **Setup**: Installs Syft tool from the official Anchore repository
2. **Analysis**: Generates MBOM for target APK file
3. **Processing**: Formats JSON output for readability
4. **Publication**: Publishes results as pipeline artifacts

### Generated MBOM Insights
The MBOM provides detailed information about:
- Package dependencies
- Component versions
- Artifact metadata
- Binary analysis results
- Package relationships

## Prerequisites

- Azure DevOps environment
- Android APK file to analyze
- Access to internet (for Syft installation)

## Getting Started

1. Clone this repository
2. Place your target APK file in the repository
3. Configure the pipeline in Azure DevOps:
   ```yaml
   trigger:
     - main

   pool:
     vmImage: 'ubuntu-latest'
   ```
4. Run the pipeline

## Pipeline Structure

The pipeline consists of three main stages:

1. **Tool Installation**
   - Downloads and installs Syft
   - Verifies installation success

2. **MBOM Generation**
   - Creates output directory
   - Analyzes APK file
   - Generates formatted JSON output
   - Verifies generated files

3. **Results Publication**
   - Publishes MBOM as pipeline artifact
   - Makes results available for download

## Tools Used

- **Syft**: Industry-standard MBOM generation tool
- **Azure DevOps**: CI/CD platform
- **jq**: JSON processing utility

## Security Benefits

- Complete software component visibility
- Enhanced supply chain security
- Dependency tracking and management
- Compliance documentation support
- Risk assessment facilitation

## Output Format

The MBOM is generated in JSON format, providing:
- Structured component data
- Detailed package information
- Version tracking
- Dependency relationships
