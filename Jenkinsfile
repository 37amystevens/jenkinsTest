#!groovy

def performGitCheckout(branch, credentialsId, codeHubRepUrl) {
    checkout([
        $class: 'GitSCM',
        branches: [
            [
                name: branch
            ]
        ],
        doGenerateSubmoduleConfigurations: false,
        extensions: [],
        submoduleCfg: [],
        userRemoteConfigs: [
            [
                credentialsId: credentialsId,
                url: "https://${codeHubRepUrl}"
            ]
        ]
    ])
}

pipeline {
  agent any
  stages {
    stage ("Init") {
      steps {
        echo "attempting to initialize sbt tool"
        echo "done initializing sbt tool"
      }
    }
    stage ("Clone Repo"){
      steps{
        echo "Cloning repository"
        performGitCheckout("master", "asteve", "github.com/37amystevens/jenkinsTest.git")
        echo "Done cloning repo"
      }
    }
    stage ("Build Repo"){
      steps{
        echo "Building project with sbt"
        def sbtHome = tool 'sbt-0.13'
        sh '{sbtHome}/bin/sbt clean'
        echo "Done cleaning project"
      }
    }
  }
}
