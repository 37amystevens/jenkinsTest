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

node {
  agent any
  tools {
    sbt 'sbt-launch'
  }
  stage ("Clone Repo"){
    echo "Cloning repository"
    performGitCheckout("master", "asteve", "github.com/37amystevens/jenkinsTest.git")
    echo "Done cloning repo"
  }
  stage ("Build Repo"){
    echo "Building project with sbt"
    sh 'sbt clean'
    echo "Done cleaning project"
  }
}
