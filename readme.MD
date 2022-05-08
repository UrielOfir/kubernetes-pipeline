
# Node.js Weight Tracker
## How to run this Azure Devops repository?

1. You need to build the enviroment with this Terraform module-
https://github.com/UrielOfir/terraform-kubernetes

2. Then you need to [add an azure devops agent to the deafult agent pool](https://docs.microsoft.com/en-us/azure/devops/pipelines/agents/v2-linux?view=azure-devops#azure-pipelines).
It must be powershell agent.

You need to add enviroment call `pool` to the azure devops envirometns.

3. You need to connect your agent machine to the kuberntes cluster with azure-cli:
`az aks get-credentials --resource-group kubernetes-resources --name kubernetes-aks1`

4. On your Azure DevOps project library, add a variable group called `common`.
Add these variables:
    
    ```
    `okta_client_id`
    `okta_client_secret`
    `okta_url`
    `pg_password` (pg= postgresql)
    `pg_username`
    `registry_url` (url of the container registry that was built by the Terraform code)
    `registry_username`
    `registry_password`
    `cookie_pwd`
    ```
***

5. Update the IP address in your application configuration in your okta account, to the ingress IP address of the kubernetes cluster. 

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
