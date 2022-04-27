
# Node.js Weight Tracker
## How to run this Azure Devops repository?
This repository builds a docker images and run it on staging and production environments by this ansible code:
https://github.com/UrielOfir/dockerAnsible.

1. You need to build the enviroment with this Terraform module-
https://github.com/UrielOfir/Terraform

2. Then you need to [add an azure devops agent to the deafult agent pool](https://docs.microsoft.com/en-us/azure/devops/pipelines/agents/v2-linux?view=azure-devops#azure-pipelines).
It must be linux agent.

You also must have an Azure container registry! 

3. Add to your pipline two enviroments: `staging` and `deployment`.  
In each enviroment add an agent on the ansible machine of your azure cloud enviroment.

4. On the deployment enviroment add a manual approval.  

4. On your Azure DevOps project library, add a variable group called `ansible`.
Add this variables:
    
    ```
    `ansible_ssh_pass` (password for the VMs that runs the app)
    `ansible_username`
    `stg_LB_ip` (LB= load balancer)
    `prd_LB_ip`
    `okta_client_id`
    `okta_client_secret`
    `okta_url`
    `pg_password` (pg= postgresql)
    `pg_username`
    `stg_pghost` (dns name of the postgresql server)
    `prd_pghost` (dns name of the postgresql server)
    `registry_url` (url of the container registry)
    `registry_username`
    `registry_password`
    ```
The code works for staging enviroment with two servers,
where the servers IPs are: 10.0.1.4 and 10.0.1.5.  
In the proudction enviroment there are three servers with IPs: 10.0.1.4, 10.0.1.5, 10.0.1.6.  
To change the hosts IPs you need to change the `hosts` in the file `azure-pipelines.yml` at `template: tools/ansible.yml`.
***

## Use docker compose on your local machine
To run this app with your local machine you need to add `.env` file to the root of the project. (you can see the instructions for `.env` file [here](https://developer.okta.com/blog/2020/06/01/node-postgres-weight-tracker)).  
Then you can run the command `docker-compose up`, and the app will be running on your local machine at port `127.0.0.1:40000`.


## About the app

This sample application demonstrates the following technologies.

* [hapi](https://hapi.dev) - a wonderful Node.js application framework
* [PostgreSQL](https://www.postgresql.org/) - a popular relational database
* [Postgres](https://github.com/porsager/postgres) - a new PostgreSQL client for Node.js
* [Vue.js](https://vuejs.org/) - a popular front-end library
* [Bulma](https://bulma.io/) - a great CSS framework based on Flexbox
* [EJS](https://ejs.co/) - a great template library for server-side HTML templates

**Requirements:**

* [Node.js](https://nodejs.org/) 14.x
* [PostgreSQL](https://www.postgresql.org/) (can be installed locally using Docker)
* [Free Okta developer account](https://developer.okta.com/) for account registration, login

## Install and Configuration

1. Clone or download source files
1. Run `npm install` to install dependencies
1. If you don't already have PostgreSQL, set up using Docker
1. Create a [free Okta developer account](https://developer.okta.com/) and add a web application for this app
1. Copy `.env.sample` to `.env` and change the `OKTA_*` values to your application
1. Initialize the PostgreSQL database by running `npm run initdb`
1. Run `npm run dev` to start Node.js

The associated blog post goes into more detail on how to set up PostgreSQL with Docker and how to configure your Okta account.

[A link to detailed blog post- Build a Weight Tracker App with Node.js and PostgreSQL](https://developer.okta.com/blog/2020/06/01/node-postgres-weight-tracker)
