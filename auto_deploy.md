# Auto deploy
> How to get branches to be built automatically when a story is moved to QA
- Create namespace in Rancher
- In the dev-kube repo:
    - Create ./resources/namespaces/**\<project\>**/qa-resources-config.yaml
    - Add project to ./resources/namespaces/cirkit/apps/cirkit/cirkit-config.yaml
    - Create sealed secret (see custom [script](https://github.com/jkovalchik/scripts/blob/master/devspace/create-secret.bat)):
    ```
    kubectl -n <namespace> create secret generic <project> --from-literal=datasource_password=<password> -o yaml --dry-run | kubeseal > resources/namespaces/<project>/<project>.sealed-secret.json && json-to-yaml.exe
    ```
    - Merge these changes all the way down to master (after CR to develop)
    - Restart cirkit
- Create the project in the docker-images repo and merge it down to develop (after CR)
- Build the **project**-builder image using the following command in the directory of the project you are building:
    ```
    make publish
    ```
- Make sure that AverittCI is a collaborator for the github repo
- Add a **.drone.yml** file to the root of the project's repo (on the develop branch)
- Activate the project in drone
## Troubleshooting
- Make sure the story is of type **Improvement** (otherwise it will just stop after the git clone in drone)
