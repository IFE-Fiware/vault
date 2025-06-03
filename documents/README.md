# Vault

## Description
This project contains the configuration files required for Vault deployment using Helm, preconfigured for use with SIMPL project.

## Pre-Requisites

Ensure you have the following tools installed before starting the deployment process:
- Git
- Helm
- Kubectl

Additionally, ensure you have access to a Kubernetes cluster where ArgoCD is installed.

The following versions of the elements will be used in the process:

| Pre-Requisites         |     Version     | Description                                                                                                                                     |
| ---------------------- |     :-----:     | ----------------------------------------------------------------------------------------------------------------------------------------------- |
| DNS sub-domain name    |       N/A       | This domain will be used to address all services of the agent. <br/> example: `*.common.int.simpl-europe.eu`   |  
| Kubernetes Cluster     | 1.29.x or newer | Other version *might* work but tests were performed using 1.29.x version   |

## Installation

Modify the values file for your preference and deploy as an usual Helm chart. 

Mentionable values:

| Variable name                 |     Example         | Description     |
| ----------------------        |     :-----:         | --------------- |
| cluster.namespace             | common      | namespace of deployment  |
| image.repository              | hashicorp/vault     | image repo  |
| image.tag                     | 1.19.0 | image tag |
| replicasCount                 | 3 | enables autocreation of topics |
| agentList                     | below the table | list of agents for which secrets should be created |
| kafkaCredentials              | user: password | additional accounts that should be created for kafka |
| hashicorp.service             | http://vaultservice.vaultns.svc.cluster.local:8200 | link to vault service
| hashicorp.role                | accessrole_name | name of role for vault access |
| hashicorp.secretEngine        | name | secret engine name in vault |
| domainSuffix                  | int.simpl-europe.eu | domain suffix
| mailpit                       | true | should secret for mailpit be created |

Example of agentList:

    agentList:
      authorities:
      - authority1
      consumers:
      - consumer01
      providers:
      - dataprovider01

All the mentioned hashicorp branch values should be populated.