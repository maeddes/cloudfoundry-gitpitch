
![Cloud Foundry](https://www.cloudfoundry.org/wp-content/uploads/2015/11/CloudFoundaryCorp_rgb.png) 

PaaS for the good ones :-)


---

## Agenda

* Intro to Cloud Foundry
* Architecture - Orgs & Spaces
* cf cli
* Apps - Buildpacks - Droplets
* manifest.yml
* Services - Service Broker API
 
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

<iframe data-src="https://www.cloudfoundry.org/membership/members/" height="380px" width="100%"></iframe>


####### https://www.cloudfoundry.org/membership/members/

---

# ARCHITECTURE

+++

## ORGS & SPACES

---

# CF CLI

+++?gist=afaae0cfafd7e2dcb4193b4d29b613e6

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

