# Auto deploy setup:
- Create namespace in Rancher
- In the dev-kube repo:
    - Create ./resources/namespaces/*<project>*/qa-resources-config.yaml
    - Create sealed secret:
        ```
        kubectl -n <project> create secret generic <project>-secret --from-literal=datasource_password=meowhow9 -o yaml --dry-run | kubeseal > <project>.sealed-secret.json && ../../../json-to-yaml.exe
        ```
- Enable project in Cirkuit:
    - Add project entry in ./resources/namespaces/cirkit/apps/cirkit/cirkit-config.yaml (cirkuit may need a restart)
- Create the project in the docker-images repo and build the *<project>*-builder docker image
- Add .drone.yml to the root of the project's repo (on the develop branch)
- Make sure that AverittCI is a collaborator for the github repo
- Activate the project in drone