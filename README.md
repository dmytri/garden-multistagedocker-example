
# Multistage Docker Example

## Example Explanation

### Question
*How might we* use a different container for the `garden test` command than for deploys or other commands.

### Why
A customer has a specific container set up for inner loop testing, but want to use a simpler container for inner loop development and deployments.

### How
Use a multistage docker container and the `targetImage` build setting.

### Steps
1. Create a Dockerfile with two stages, build-test, and build-deploy, that both extend a common base image
1. Add something that is only available for `garden test` to the build-test target, in this example `npm`
1. Create a variable target-image and set it to build-test when `garden test` is run, build-deploy otherwise
1. add a test called install that uses `npm` (only available in build-test target)
1. disable this test if target-image is not build-test

## Running Example

### Requires
minikube or other local kubernetes

#### Command
`garden dev`

#####  Expected Result
- unit test passes
- npm-not-installed test passes
- npm-installed test is skipped
- install test is skipped

#### Command
`garden test`

##### Expected Result
- unit test passes
- npm-not-installed is skipped
- npm-installed test passes
- install test passes

## See
- [site/Dockerfile](site/Dockerfile)
- [site/garden.yml](site/garden.yml)
- [https://docs.garden.io/reference/module-types/container#build.targetimage](https://docs.garden.io/reference/module-types/container#build.targetimage)
- [https://docs.garden.io/reference/template-strings/modules#usd-command.name](https://docs.garden.io/reference/template-strings/modules#usd-command.name)

