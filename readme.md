![https://travis-ci.org/allthingsclowd/WebPageCounterInProduction.svg?branch=master](https://travis-ci.org/allthingsclowd/WebPageCounterInProduction.svg?branch=master)

# Web Page Counter - A Production Grade Deployment

Modify this [repository](https://github.com/allthingsclowd/web_page_counter) as follows :

Where possible leverage cloud services as opposed to 'rolling you own' e.g. if the cloud provider offers a Redis service then consume it!
Use HashiCorp's Terraform, infrastructure provisioning tool, to deploy the WebPageCounter application in the following phases

__Phase 1 : Production Grade Infrastructure in a Single Region__
Consul, Vault and Nomad should be deployed in a public cloud (Azure, AWS or GCP) in a single region and TLS should be used on all endpoints. Ensure that hardware failure domains are considered during this deployment.

__Phase 2 : Production Grade Infrastructure in a Multi Region Cloud__

__Phase 3 : High Availablity with a focus on Disaster Recovery

__Phase 4 : High Availablity with a focus on Performance

__Phase 5 : Introduce a second Public Cloud to Create a Multi Region Multi Cloud Deployment

## TODO

### Refactor



### New Features



## Done
* Build own box using packer with above scripts
* Upload to vagrantcloud
* Update Vagrant file to consume the new box
* Add a Consul(1) server 
* Remove scripts from Packer and link back to repo master scripts, use SCRIPTS feature
* Add 'manual' test scripts to TravisCI
   * source env file
   * over write variables for local redis 
   * use `curl` to verify app returns http 200 & exit 0
   * use `lynx --dump` to capture counter updates between refreshes
   * Add TravisCI for Go APP
* scripted added to read in var.env and upload to consul
* main.go modified to use consul for variables when it's present
* Add a Vault (1) server
* if golang app can't reach redis or any other error return a zero
* if consul is not up - fallback to var.env values
* update goapp to have a /health to provide the status of it's services (text only)
   * GOOD
   * NOTGOOD
* Register Redis on Consul  
   What: Register the redis service on consul  
   Why: So the GOApp can connect dynamically (discover) the service  
  
   How: Check ping, write a dummy k/v, read the dummy k/v  
* Register Go App in Consul  
   What: Register the goapp service on consul  
   Why: So the webtier (NGINX) can connect dynamically (discover) the service  
  
   How: Check the website is up & the /health url returns GOOD  
      * update goapp consul healthcheck to expect GOOD/NOTGOOD  
* Make readme pretty (again)  
* Make goAPP use consul to find redis port and ip  
* Make nginx use consul to populate the conf file (consul-template)
* 3 IPs per godev machine main.go using ip1:8080, ip2:8080, ip3:8080
* WRONG: Modify existing goapp to listen and respond on 3 ports -8081, 8082, 8083 (3 x gorountines)
 3 separate main.go instances on the one server
* If running on travis only create a single listener on port 8080
* Update Consul service healthcheck to accomodate new changes
* Update NGINX Consul-template to receive updates
* Update Travis to new requirements
* Repeat all of the above with a 2nd instance of the goapp server
* Sign up for Datadog trial account using a gmail alias e.g. <bob@gmail.com> becomes <bob+datadogtrial@gmail.com>
* Install DDog Agent on the Macbook and test using Guages & Counters
* Update application to submit datadog pagecount counter once redis has been successfully updated
* Add datadog guage that reports on the number of available goapp services
* Remove redis02 and vault servers - not required yet!
* Create another Datadog Test Account for the 5 servers
* Install datadog agent on all servers
* Update consul-template nginx routine to include goapp service guage routine
* Rollback to a single network ip on the vagrantfile
* Don't execute the goapp upon installation - nomad will be used to do this later
* Write a nomad job using the raw_exec driver (NOT DOCKER) to launch the application ONCE on any node
* Add tag that includes port details to ddog metric
* Add service checks/tests to nomad job
* Move all logs to `/vagrant/logs/`
* Add UI ability to terminate current go-app service - facilitate quicker nomad demo - either add button to main page or create new endpoint feature
* Add github templates
* Add Travis Deployment on Tags
* Update App deployment to use releases
* Backout the unauthorised architectural switch from Vault v1 Secrets to v2 Secrets (versioned)
* UNDO :Move Redis Password into VAULT KV - demonstrates best practice of using centralised secret management vault - time 4 hrs
* - modify vault installation to make binary accessable on all nodes
* - install envconsul on all nodes
* - auto-generate redis password on leader node and store in vault using vault client (binary)
* - update redis installation to utilise consul-template to get redis password from vault
* - revert main.go application to consume vault v1 secrets (unversioned)
* - Add Vault App-Role to Application__ for Vault Access Method - demonstrates best practice of using centralised secret management vault - time est: 4hrs
* AddDataDog event when crash occurs e.g. “app 8081 crashed” - provides enhance reporting metrics - time est:2hrs
* [Moved to it's own repo as requirement does not belong here](https://github.com/allthingsclowd/vault_versus_consul) Metrics: Consul KV versus Vault KV. Test with 100-1000 entries. Simple bash script timed - see if there's a significant overhead when using vault as a KV over Consul KV. - time est: 4hrs


