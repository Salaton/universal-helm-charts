# universal-helm-charts

## Overview

This work aims to streamline Kubernetes deployments across multiple services by reducing code duplication and ensuring consistency. This umbrella Helm chart encapsulates common configurations and functionalities, facilitating a DRY (Don't Repeat Yourself) approach and simplifying Kubernetes deployments.

The repo is structured into two main parts:

-   **Library Chart**: Contains reusable definitions and templates for common Kubernetes resources.
-   **Base Chart**: Utilizes the library chart to provide a standardized deployment template for applications.

This approach simplifies the Kubernetes deployment process, enabling rapid and consistent deployments across various environments and services.

## Structure

-   `library/`: A Helm library chart containing templates for common Kubernetes resources like ConfigMaps and HPAs.
-   `base-chart/`: A Helm chart that serves as the base for deploying microservices. It includes the library chart as a dependency.

## Features

- **Centralized Configuration**: Manage common configurations across all microservices in one place.
- **Modular Design**: Extend and customize configurations to meet the specific needs of each microservice.
- **Scalability**: Designed to support deployments of any scale, from small to large enterprises.
- **Best Practices**: Integrates Kubernetes and Helm best practices to provide a solid deployment foundation.

## Getting Started

### Prerequisites

- Helm version 3.x or later
- Access to a Kubernetes cluster
- Basic knowledge of Kubernetes and Helm concepts

### Installation

1. Clone the repository:
   ```bash
   git clone git@github.com:Salaton/universal-helm-charts.git
   cd universal-helm-charts
   ```
 2. Install the Helm chart:
	```bash
	helm install my-microservices ./unified-chart -f custom-values.yaml
	```
	Replace my-microservices with your deployment name and `custom-values.yaml` with 		your specific configuration file.
	
 ### Usage
To deploy a microservice using the base chart, you can define your service-specific configurations in a `values.yaml` file. For example:
```yaml
configMap:
  name: myservice-config
  data:
    setting1: "value1"

hpa:
  enabled: true
  name: myservice-hpa
  targetRef:
    name: myservice
  minReplicas: 2
  maxReplicas: 5
  metrics:
    - type: Resource
      resource:
        name: cpu
        target:
          type: Utilization
          averageUtilization: 75

```
Then, deploy your microservice using Helm:
```bash
`helm install myservice ./base-chart -f values.yaml`
```