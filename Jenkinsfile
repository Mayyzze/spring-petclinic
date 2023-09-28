@Library('sastScaScan') _
pipeline {
    agent any

    parameters {
        choice(name: 'PROMOTION_TYPE', choices: ['stage-release', 'build'], description: 'Select an option')

    }

    stages {
        stage('Stage-Release') {
            when {
                expression { params.PROMOTION_TYPE == 'stage-release' }
            }
            steps {
                script {
                    // Ask for the third parameter if the choice parameter is populated
                    input message: 'Please provide the source branch', parameters: [string(name: 'SR_SOURCE_BRANCH', description: 'Source Branch')]
                }
                echo "SOURCE_BRANCH is ${params.SR_SOURCE_BRANCH}"
            }
        }

        stage('Build') {
            when {
                expression { params.PROMOTION_TYPE == 'build' }
            }
            steps {
                script {
                    input message: 'Please provide the source branch of the build version creation', parameters: [string(name: 'BUILD_SOURCE_BRANCH', defaultValue: '', description: 'Source Branch')]
                    input message: 'Please provide the destination branch of the build version creation', parameters: [string(name: 'BUILD_DEST_BRANCH', defaultValue: '', description: 'Destination Branch')]
                }
                echo "Building with CHOICE_PARAM: ${params.PROMOTION_TYPE}, BUILD_SOURCE_BRANCH: ${params.BUILD_SOURCE_BRANCH}, BUILD_DEST_BRANCH: ${params.BUILD_DEST_BRANCH}"
            }
        }
    }
}

