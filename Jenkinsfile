#!/usr/bin/env groovy

node('master') {

    try {

        stage('build') {
            // Clean workspace
            deleteDir()
            // Checkout the app at the given commit sha from the webhook
            checkout scm
        }

        stage('test') {
            // Run any testing suites
            sh "echo 'TESING PHASE'"
        }

        stage('deploy') {
            sh "echo 'DEPLOYING PHASE'"
            wrap([$class: 'AnsiColorBuildWrapper', colorMapName: "xterm"]) {
                ansibleTower(
                    towerServer: 'Ansible AWX',
                    jobTemplate: 'Minecraft',
                    importTowerLogs: true,
                    inventory: '',
                    jobTags: '',
                    limit: '',
                    removeColor: false,
                    verbose: true,
                    credential: '',
                    extraVars: ''
                )
            }
        }

    } catch(error) {
        throw error

    } finally {
        // Any cleanup operations needed, whether we hit an error or not

    }
}
