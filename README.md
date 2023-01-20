## GITHUB WORKFLOWS

This repository keeps the workflows used in konstellation projects like kdl-server and kre (coming soon). This allows us not to repeat code in our other projects. This is not a workflow template.

It also contains those workflows that are used as [required workflows](https://docs.github.com/en/actions/using-workflows/required-workflows).

### CI Templates

1. [helm-release](./.github/workflows/helm-release.yaml): Allow us to generate a new chart helm release (release candidate or fix inside a release branch). 
Inputs and secrets:
    - `chart_file`: The path to Chart.yaml helm file to update.
    - `github_token`: The token with privileges to write in the repository.
    - `chart_url`: Chart repo URL.
    - `chart_path`: Chart path to zip in the release.

2. [new-release](./.github/workflows/new-release.yaml): This workflow allow us to generate a new release branch and tag and update the chart version.
Inputs and secrets:
    - `chart_file`: The path to Chart.yaml helm file to update.
    - `github_token`: The token with privileges to write in the repository.
    - `chart_url`: Chart repo URL.
    - `chart_path`: Chart path to zip in the release.

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

5. [helm-lint](./.github/workflows/helm-lint.yaml): Execute a helm lint on a chart repository to validate the configuration. You must to have a `ct.yaml` file configured and a `helmlintconf.yaml` file in your repository root to validate the rules.

## Required workflow

1. [secrets-scanning.yml](./.github/workflows/secrets-scanning.yml): This workflow is used to scan the repository for secrets and alert us if there are any.

### References
- https://docs.github.com/en/actions/learn-github-actions/reusing-workflows
- https://docs.github.com/en/actions/learn-github-actions/workflow-syntax-for-github-actions#onworkflow_callinputs
- https://docs.github.com/en/actions/learn-github-actions/workflow-syntax-for-github-actions#onworkflow_callsecrets
- https://docs.github.com/en/actions/learn-github-actions/workflow-syntax-for-github-actions#jobsjob_idstepsuses
- https://github.com/helm/chart-testing-action
- https://github.com/helm/chart-testing


