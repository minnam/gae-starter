# Prerequisite
  Prepare 3 branches; master, staging, develop

# Basic Deployment Setup
1. Install `gcloud`, run `npm install -g gcloud`
1. Create a project by running `gcloud app create` or in this link https://console.cloud.google.com/projectcreate
1. Copy and paste config-files into the project repo and change PROJECT_NAME to your project name
1. Run `gcloud app deploy`

## Details
- This setting creates 2 instances. Production and Staging. We assume that project repo will have 3 major repo; `master`, `staging`, `develop`. Every new feature will be merged to develop and then there will be a pull request from `develop` to `staging`. When there is an activity with `staging` repo, the build will be triggered in GAE. When `staging` instance works well, there can be a pull request from `staging` to `master` which triggers build to the production instance.


# Build Trigger Setup for Staging
1. Go to your project and navigate to https://console.cloud.google.com/cloud-build/triggers
1. Click `Create Trigger`
1. Name your trigger, `PROJECT_NAME-staging`
1. Set Event to `Pull Request`
1. Set Repository (you can link your github)
1. Set Source Branch to `staging`
1. Set Build configuration to `Cloud Build Configuration file (yaml or json)`
1. Set Cloud Build Configuration file location to /cloudbuild.staging.yaml
1. Set the Substitution variable if needed (this is environment variables). Variables must start with _ here and also in the app. Ex. `_DB_PASS`
1. Test triggers by creating pull requests.

# Build Trigger Setup for Production
1. Same procedures as staging but change name and target files for `prod` and target `master` instead of `staging`

