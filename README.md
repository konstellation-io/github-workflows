## GITHUB WORKFLOWS

This repository keeps the different workflows used in konstellation projects like kdl-server and kre (comming soon). This allow us to not repeat code in our different projects. This is not a workflow template.

### Templates

1. [helm-release](./.github/workflows/helm-release.yaml): Allow us to generate a new chart helm release (release candidate or fix inside a release branch). 
Inputs and secrets:
    - `chart_file`: The path to Chart.yaml helm file to update.
    - `github_token`: The token with privileges to write in the repository.

2. [new-release](./.github/workflows/new-release.yaml): This workflow allow us to generate a new release branch and tag and update the chart version.
Inputs and secrets:
    - `chart_file`: The path to Chart.yaml helm file to update.
    - `github_token`: The token with privileges to write in the repository.

3. [lint-dockerfile](./.github/workflows/lint-dockerfile.yaml): This passes the hadolint tool to validate the Dockerfile.
Inputs:
    - `component_path`: The directory path of the dockerfile to pass hadolint.

4. [build](./.github/workflows/build.yaml): Generate a release/fix tag for each component that uses this template, build the image and update the chart values with the new version. It's used to generate a new appversion if the principal app changes.
Inputs and secrets:
    - `component`: Component name to generate a new rc or fix.
    - `component_helm_tag`: Naming used in the chart values yaml to update with the new component tag value.
    - `component_path`: Path to the Dockerfile to build the image.
    - `component_image`: Used to push the image to dockerhub or another registry with this name.
    - `component_app`: To identify the principal application to update the chart appversion.
    - `chart_file`: The path to Chart.yaml helm file to update.
    - `values_file`: The path to values.yaml helm file to update the components.
    - `pat`: The token with privileges to write in the repository. (be carefull if you are using branch rules)
    - `docker_username`: The username to push the image to the registry.
    - `docker_token`: The token used to authenticate and allow us to push the image into the registry.

4. [chart-release](./.github/workflows/chart-release.yaml): Generate a helm chart release.
Inputs and secrets:
    - `chart_url`: Chart repo URL.
    - `chart_path`: Chart path to zip in the release.

### References
- https://docs.github.com/en/actions/learn-github-actions/reusing-workflows
- https://docs.github.com/en/actions/learn-github-actions/workflow-syntax-for-github-actions#onworkflow_callinputs
- https://docs.github.com/en/actions/learn-github-actions/workflow-syntax-for-github-actions#onworkflow_callsecrets
- https://docs.github.com/en/actions/learn-github-actions/workflow-syntax-for-github-actions#jobsjob_idstepsuses

