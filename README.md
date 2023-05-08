# NextJs continus deployment exemple on OVH VPS.

The concerned script is located in **.github/workflows/main.ym**

What is doing this script? 

- The script is launch on event that is triggered when main branch is push from a local environnement.
- It first Start an ubuntu environment on github action to run the project.
- In this new Ubuntu instance, it checkout the code by using actions/checkout.
- Then launch project dependencies installation.
- Then launch project build which has next.config.js that specify the build output file ( build/)
- Use scp-action dependency to :
    - remove files from the VPS.
    - copy the build folder directly into a target folder on the vps server.(You can replace by cdn if you want).

The **with:** instruction give necessary environment variables for the dependency **appleboy/scp-action**. This dependency is copying output folder (build/) into a target by using scp (secure copy protocole).

Environment variables has to be set on github into concerned repository: 
 - **settings > secrets and variables > action** > Use the green button **"new repository secret"** to add each variable like so:

![Action Secrets](/readme-assets/secrets.png "Action Secrets")


When the pipeline success:

![Pipeline Success](/readme-assets/pipeline-success.png "Pipeline Success")