#!/usr/bin/env groovy

BRANCH = env.BRANCH
node {
    stage('Checkout, build and push specified branch') {
        directoryName = BRANCH.replaceAll("/","_")
        dir("${directoryName}") {
            buildAndPush(BRANCH)
        }
    }
}

def buildAndPush(branch) {
    checkout([$class: 'GitSCM',
             branches: [[name: "*/${branch}"]],
             doGenerateSubmoduleConfigurations: false,
             extensions: [[$class: 'WipeWorkspace'],
                          [$class: 'LocalBranch', localBranch: '**']],
                           submoduleCfg: [],
                           userRemoteConfigs: [[url: 'https://github.com/gravitational/docker-ubuntu.git']]])
    sh 'make images'
    sh 'make push'
}