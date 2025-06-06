# SonarQube Azure DevOps Pipeline Integration

## Overview

This project provides an Azure DevOps pipeline integration with SonarQube Community Edition to enable static application security testing (SAST) for application code and infrastructure-as-code (IaC).  
The pipeline automatically scans source code during the CI/CD process and publishes results to a SonarQube project dashboard.

---

## How It Works

- Installs Python and project dependencies (`requirements.txt`).
- Downloads and runs SonarScanner CLI.
- Analyzes files based on patterns specified in the `sonar-project.properties` file.
- Supports scanning:
  - Python code (`*.py`)
  - YAML files (`*.yml`, `*.yaml`)
  - Dockerfiles
  - Terraform files (`*.tf`)
- Uploads vulnerabilities, bugs, code smells, and security hotspots to SonarQube.
- Results are visible in the configured SonarQube project dashboard.

---

## Setup Instructions

1. **Create a New SonarQube Project**
   - Go to [SonarQube](https://sonarqube.cccudev.org) and create a new project.
   - Save the `projectKey`.

2. **Update the `sonar-project.properties` File**
   - Set `sonar.projectKey` to your new project key.
   - Set `sonar.sources=.` to scan the entire repository.
   - Set `sonar.inclusions=**/*.py,**/*.yml,**/*.yaml,**/Dockerfile,**/*.tf` to include relevant file types.

3. **Configure SONAR_TOKEN**
   - Use the existing Azure DevOps Variable Group (`SonarQubeVars`).
   - If needed, create a new token under **My Account > Security** in SonarQube and update the variable group.

4. **Use the Existing Azure Pipeline**
   - No changes needed to `azure-pipelines.yml` unless customization is required.
   - The pipeline automatically runs on push or pull request events (branch trigger configurable).

5. **View Results**
   - After the pipeline completes, view your project's results in SonarQube under the assigned project key.

---

## Current Functionality

- Python code scanning (SAST)
- YAML, Dockerfile, and Terraform scanning for code quality and security risks
- Vulnerability detection
- Code smell and bug identification
- Security hotspot detection
- Seamless integration with Azure DevOps pipelines

---

## Future Enhancements (Optional)

- Integrate secrets scanning (e.g., Gitleaks) to detect hardcoded credentials
- Add container image scanning (e.g., Trivy, Grype)
- Implement SonarQube Quality Gates to block merges on critical issues
- Introduce policy-as-code scanning for Kubernetes and Terraform

---
