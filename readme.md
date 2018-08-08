![https://travis-ci.org/allthingsclowd/WebPageCounterInProduction.svg?branch=master](https://travis-ci.org/allthingsclowd/WebPageCounterInProduction.svg?branch=master)

# Web Page Counter - A Production Grade Deployment

Modify this [repository](https://github.com/allthingsclowd/web_page_counter) as follows :

Where possible leverage cloud services as opposed to 'rolling you own' e.g. if the cloud provider offers a Redis service then consume it!
Use HashiCorp's Terraform, infrastructure provisioning tool, to deploy the WebPageCounter application in the following phases

__Phase 1 : Production Grade Infrastructure in a Single Region__
Consul, Vault and Nomad should be deployed in a public cloud (Azure, AWS or GCP) in a single region and TLS should be used on all endpoints. Ensure that hardware failure domains are considered during this deployment.

__Phase 2 : Production Grade Infrastructure in a Multi Region Cloud__

__Phase 3 : High Availablity with a focus on Disaster Recovery__

__Phase 4 : High Availablity with a focus on Performance__

__Phase 5 : Introduce a second Public Cloud to Create a Multi Region Multi Cloud Deployment__

## TODO

### Refactor



### New Features



## Done



