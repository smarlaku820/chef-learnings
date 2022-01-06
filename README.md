# Configuration Management & Automation

- Why automate ? 
- Automation tools adopt a declarative approach. Imperative vs Declarative Styles

## Models of configuration management tools - Push vs Pull

Push based models - ansible and saltstack

A master server pushes the configurations/software to individual servers. configuration push is initiated by the master nodes.

Pull based models - puppet and chef

The individual servers contact the master server on regular intervals.
- establish a connection
- download the software update & configure themselves accordingly
- config pull is initiated by agents on the remote nodes at regular intervals


## Characteristics of Automation Tools - Idempotency and Covergence

These characteristics of automation tools help you declare and achieve a specific desired state.
Idempotency is a behaviour in which same result is yeilded even you perform it 'x' number of times.
Convergence means bringing it together. ie., you may be performing a series of idempotent tasks but the objective is to settle things in perfect final state.
Idempotent means not taking actions when they aren't needed, convergent means it "settles" on a specific final state.

# Chef - Automation Tool

The foundation of chef is established in 2008. (Initially OpsCode renamed as Chef)
Multiple products
- Chef automate
- Chef Infrastructure Automation tool or Simply Chef tool.
- Chef Inspec
- Chef Habitat

Chef is Ruby based, system automation friendly IT Automation tool used to deploy, manage and orchestrate various apps and services across your infrastructure.

Why Chef ?
- Uses declarative programming approach.
- The primary responsibility of chef is to maintain the defined state. (Desired state configuration)
- Chef helps in maximizing the business productivity
- Code is Idempotent
- Chef is highly scalable

Usecases - Simple
- Installing application on single server (WebServers, Databases, Firewall, Tools/Application)
Usecases - Complex
- Scenarios can include infrastructure across private(vmware, openstack) and public cloud (Amazon/Azure/GCP)
- Deploy | Configure | Orchestrate Application
- Chef is supported as Managed Service in public clouds

## The Chef way - 

### Creating a user
```
user 'sam' do
    action :create
end
```
### Creating a file - 
```
file '/tmp/test' do
    content "This is a test file\n"
    action :create
end
```
### Removing a user
```
user 'sam' do
    action :remove
end
```
### Removing a file
```
file '/tmp/test' do
    content "This is a test file\n"
    action :delete
end
```
### Install & Configure a Web Server
```
# web server package installation
package 'httpd' do
    action :install
end

# web server file configuration
file '/var/www/html/index.html' do
    content "This is my chef configured web server file"
    action :create
end

# web server service startup
service 'httpd' do
    action :start
end
```

## Chef Architecture

Chef server can only be linux. The Clients however can be any OS flavours.

Chef deployment models.
- Server-Client model (for production use cases)
- Standalone or Chef-Zero model (development/testing/POC's - chef cookbooks)

There are 3 main sections
- Chef workstation -> Local development platform (create/test/apply/upload chef codes) -> Chefdevk (Chef development kit)
- Chef Server -> Chef code is managed. Hub for Configuration data. Chef workstation pushes cookbooks to chef server. Chef clients communicate with
                 Chef server to get the chef code or configuration updates. 
- Chef Client/Nodes