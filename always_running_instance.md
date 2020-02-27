# Always running instance setup
- In the dev-kube repo:
    - Create ./resources/namespaces/**\<project\>**/apps/dev-**\<project\>**
    - Inside the dev-**\<project\>** create the following files:
        - deployment.yaml
        - ingress.yaml
        - pvc.yaml
        - service.yaml
- Add the **build-dev** and **patch-dev** steps to the project's **.drone.yml** file (use a similar project as a reference)
