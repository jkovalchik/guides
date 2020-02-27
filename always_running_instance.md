# Always running instance setup
- Add the **build-dev** and **patch-dev** steps to the project's **.drone.yml** file (use a similar project as a reference)
- Merge this down to develop so the **push** event triggers a build of the project and uploads the image to Nexus
    - This image is needed for the dev instance to build
- In the dev-kube repo:
    - Create ./resources/namespaces/**\<project\>**/apps/dev-**\<project\>**
    - Inside the dev-**\<project\>** create the following files:
        - deployment.yaml
        - ingress.yaml
        - service.yaml
