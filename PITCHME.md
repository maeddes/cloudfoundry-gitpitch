
![Cloud Foundry](https://www.cloudfoundry.org/wp-content/uploads/2015/11/CloudFoundaryCorp_rgb.png) 

PaaS for the good ones :-)


---

## Agenda

* Intro to Cloud Foundry
* Access control
* cf cli
* Apps - Buildpacks - Droplets
* cf push & manifest.yml
* Services - Service Broker API
 
---

## Sources

 * docs.cloudfoundry.org
 
--- 

# INTRO

+++

## Some facts

* First released in 2011
* Open Cloud Native Platform / Platform as a Service
* Fast and easy to build, test, deploy & scale apps
* Works with many languages or frameworks
* Available as open source, commercial distributions or hosted offerings

+++

## Here is my source code 
## Run it on the cloud for me 
## I do not care how

A haiku dedicated to ‘cf push’ by Onsi Fakhouri, Pivotal

+++

<iframe data-src="https://www.cloudfoundry.org/membership/members/" height="480px" width="100%"></iframe>

 https://www.cloudfoundry.org/membership/members/

+++

IaaS / PaaS Taxonomy

![Cloud Stack](https://docs.cloudfoundry.org/concepts/images/power-of-platform.png)

(Source: docs.cloudfoundry.org)

+++

## PaaS Concepts

* Anyone can deploy applications quickly and make them accessible for everybody
* In case of high requests, the platform can scale the app easily
* Focus is on application an it's logic - not the underyling infrastructure

+++

## How the Cloud Balances Its Load

Clouds balance their processing loads over multiple machines, optimizing for efficiency and resilience against point failure. A Cloud Foundry installation accomplishes this at three levels:

* BOSH creates and deploys virtual machines (VMs) on top of a physical computing infrastructure, and deploys and runs Cloud Foundry on top of this cloud. To configure the deployment, BOSH follows a manifest document.
* The CF Cloud Controller runs the apps and other processes on the cloud’s VMs, balancing demand and managing app lifecycles.
* The router routes incoming traffic from the world to the VMs that are running the apps that the traffic demands, usually working with a customer-provided load balancer.

---

# Access Control

+++

## Orgs

An org is a development account that an individual or multiple collaborators can own and use. All collaborators access an org with user accounts. Collaborators in an org share a resource quota plan, applications, services availability, and custom domains.

By default, an org has the status of active. An admin can set the status of an org to suspended for various reasons such as failure to provide payment or misuse. When an org is suspended, users cannot perform certain activities within the org, such as push apps, modify spaces, or bind services. For details on what activities are allowed for suspended orgs, see Roles and Permissions for Suspended Orgs.

+++

## Spaces

Every application and service is scoped to a space. Each org contains at least one space. A space provides users with access to a shared location for application development, deployment, and maintenance. Each space role applies only to a particular space.

+++

## User Accounts
A user account represents an individual person within the context of a CF installation. A user can have different roles in different spaces within an org, governing what level and type of access they have within that space.

+++

## Roles and Permissions
A user can have one or more roles. The combination of these roles defines the user’s overall permissions in the org and within specific spaces in that org.

+++

## Domains

* The term domain in this topic differs from its common use and is specific to Cloud Foundry. 
* The use of domain name, root domain, and subdomain refers to DNS records.
* Domains indicate to a developer that requests for any route created from the domain will be routed to Cloud Foundry.

+++

## Quotas

Default Quota Plan for an Org

* Memory Limit: 10240 MB
* Total Routes: 1000
* Total Services: 100
* Non-basic Services Allowed: True
* Trial DB Allowed: True

---

# CF CLI

+++?gist=afaae0cfafd7e2dcb4193b4d29b613e6

+++

## Targets

```bash
$ cf login -a https://api.example.com -u username@example.com
API endpoint: https://api.example.com

Password>
Authenticating...
OK

Select an org (or press enter to skip):
1. example-org
2. example-other-org

Org> 1
Targeted org example-org

Select a space (or press enter to skip):
1. development
2. staging
3. production

Space> 1
Targeted space development
```

+++

##Login

- Upon successful login, the cf CLI saves a config.json file containing your API endpoint, org, space values, and access token. If you change these settings, the config.json file is updated accordingly.

- By default, config.json is located in your ~/.cf directory. The CF_HOME environment variable allows you to locate the config.json file wherever you like.

+++

...

---

Applications, Buildpacks & Droplets

+++

https://docs.cloudfoundry.org/buildpacks/
https://github.com/cloudfoundry-community/cf-docs-contrib/wiki/Buildpacks#community-created

+++

!(https://1.bp.blogspot.com/-4aQw8F8suu4/VrkvObvIjkI/AAAAAAAAG08/X3At9XP5A9k/s1600/Selection_019.png)

(source: http://nanduni.blogspot.de)

+++

## Container image goes here

+++

# cf push

+++

```bash
mhs@R2-D2:~$ cf push --help
NAME:
   push - Push a new app or sync changes to an existing app

OPTIONS:
   -b                           Custom buildpack by name (e.g. my-buildpack) or Git URL (e.g. 'https://github.com/cloudfoundry/java-buildpack.git') or Git URL with a branch or tag (e.g. 'https://github.com/cloudfoundry/java-buildpack.git#v3.3.0' for 'v3.3.0' tag). To use built-in buildpacks only, specify 'default' or 'null'
   -f                           Path to manifest
   --health-check-type, -u      Application health check type (Default: 'port', 'none' accepted for 'process', 'http' implies endpoint '/')
   -i                           Number of instances
   -k                           Disk limit (e.g. 256M, 1024M, 1G)
   -m                           Memory limit (e.g. 256M, 1024M, 1G)
   --no-manifest                Ignore manifest file
   --no-route                   Do not map a route to this app and remove routes from previous pushes of this app
   --no-start                   Do not start an app after pushing
   -p                           Path to app directory or to a zip file of the contents of the app directory
   -t                           Time (in seconds) allowed to elapse between starting up an app and the first healthy response from the app

ENVIRONMENT:
   CF_STAGING_TIMEOUT=15        Max wait time for buildpack staging, in minutes
   CF_STARTUP_TIMEOUT=5         Max wait time for app instance startup, in minutes
```





---

# SERVICES

+++

```bash
$ cf
[..]
SERVICES:
   marketplace                            List available offerings in the marketplace
   services                               List all service instances in the target space
   service                                Show service instance info

   create-service                         Create a service instance
   update-service                         Update a service instance
   delete-service                         Delete a service instance
   rename-service                         Rename a service instance

   create-service-key                     Create key for a service instance
   service-keys                           List keys for a service instance
   service-key                            Show service key info
   delete-service-key                     Delete a service key

   bind-service                           Bind a service instance to an app
   unbind-service                         Unbind a service instance from an app

   bind-route-service                     Bind a service instance to an HTTP route
   unbind-route-service                   Unbind a service instance from an HTTP route

   create-user-provided-service           Make a user-provided service instance available to CF apps
   update-user-provided-service           Update user-provided service instance

```
---

#Test & Backup

+++?gist=8da53731fd54bab9d5c6

+++?gist=28ee3d19ddef9d51b15adbdfe9ed48da

+++?gist=cf4227416b55dac54a53

+++?gist=afaae0cfafd7e2dcb4193b4d29b613e6

+++

As Kanye West said:

> We're living the future so
> the present is our past.

+++

```javascript
function fancyAlert(arg) {
  if(arg) {
    $.facebox({div:'#foo'})
  }
}
```

+++

```
No language indicated, so no syntax highlighting. 
But let's throw in a <b>tag</b>.
```

+++

```
No language indicated, so no syntax highlighting. 
But let's throw in a <b>tag</b>.
```

+++

```shell
$ cf
NAME:
   C:\Program Files\CloudFoundry\cf.exe - A command line tool to interact with Cloud Foundry

USAGE:
   C:\Program Files\CloudFoundry\cf.exe [global options] command [arguments...] [command options]
```

+++

```bash
$ cf
NAME:
   C:\Program Files\CloudFoundry\cf.exe - A command line tool to interact with Cloud Foundry

USAGE:
   C:\Program Files\CloudFoundry\cf.exe [global options] command [arguments...] [command options]
```

