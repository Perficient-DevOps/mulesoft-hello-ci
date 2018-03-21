/*
This pipeline build example is for a Nodejs application.  The stages within this pipeline will build the app, package the app
into a zip file, perform a Nexus IQ scan, then call a downstream job to deploy the app to an environment.  These builds are
considered to be throw away as no GIT tag is created and the build is not stored in Nexus Repo.  This build is intended to
be a developer quick test.

Authors:
Sean Wilbur (sean.wilbur@perficient.com)
Geoff Rosenthal (geoffrey.rosenthal@perficient.com)

© 2018 Perficient, Inc. All Rights Reserve
*/

//Leverage Jenkins shared library
@Library('jenkins-shared-library') _

pipeline{
  //Assume nodes for mulesoft
  agent { label 'mulesoft' }

  options {
    disableConcurrentBuilds()
    // prevents checkout from automatically happen on deployment nodes
    skipDefaultCheckout()
  }

  environment {
    // Globally Defined

    // Provide application specific name for use in Nexus
    NEXUS_ARTIFACTID="hello-ci"

    // variables used during build
    ARTIFACT_FILENAME=""
    DEPLOY_ENV=''
    TARGET_APPLICATION=""
    TARGET_VERSION=""

  }//End environment

  triggers {
    // Poll SCM every 15 minutes for changes
    pollSCM('H/15 * * * *')
  }

  stages{

    stage( "Clean WorkSpace" ) {
      // Cleanup the workspace to start from scratch
      steps{
        cleanWs()
      }
    }//End Clean WorkSpace

    stage( 'Checkout Source' ) {
    //Checkout source code from GIT
      steps{
        // workaround to get GIT plugin environment Variables, we need to collect the checkout command output, which is a map that contains them
        // https://issues.jenkins-ci.org/browse/JENKINS-35230
          script{
            scm_map = checkout scm
            GIT_BRANCH = scm_map['GIT_BRANCH']
            // get just the branch name minus the remote only splitting on first
            // match in case the rest of the branch has more '/' chars.
            GIT_BRANCH_NAME = GIT_BRANCH.split('/',2)[1]
          }
          sh "echo 'Checkout of GIT branch: ${GIT_BRANCH}'"
          sh "echo 'GIT_BRANCH_NAME: ${GIT_BRANCH_NAME}'"
        }
    }//End Checkout Source

  	stage( "Setup Environment Variables" ) {
    //Setup environment variables to be used later in build.  In this example, Jenkins was used for deployment.  Deployment target Environment
    //was based upon which branch build was created from.
      steps{
        script {
          //Find and store semantic version as specified in package.json to use to create build version label
          def props = readPOM file: 'pom.xml'
          def version = props['version']
          //Define unique build version
          TARGET_VERSION = "$version-$BUILD_TIMESTAMP_STRING"
          ARTIFACT_FILENAME="${NEXUS_ARTIFACTID}-${VERSION_TAG}.zip"
          // modify build name to match
          currentBuild.displayName = "${TARGET_VERSION}"
        } // end script
        // output some information about the environment we just setup
        sh "echo 'version: ${TARGET_VERSION}'"
        sh "echo 'artifact_filename: ${ARTIFACT_FILENAME}'"
        sh "echo 'deploy_env: ${DEPLOY_ENV}'"
        sh "echo 'target_application: ${TARGET_APPLICATION}'"
      }
    }//End Setup Environment Variables

    stage( 'Maven Package' ) {
      steps{
        sh 'mvn package'
      }
    }

  }//end stages
}//end pipeline
