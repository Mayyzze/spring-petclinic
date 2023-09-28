@Library('sastScaScan') _

def getPromotionChoices() {
    return ['stage-release', 'build']
}

pipeline {
    agent any

    parameters {
        [$class: 'ChoiceParameter', 
         choiceType: 'PT_SINGLE_SELECT', 
         filterLength: 1, 
         filterable: false, 
         name: 'PROMOTION_TYPE', 
         script: [
             $class: 'GroovyScript', 
             fallbackScript: [
                 classpath: [], 
                 sandbox: false, 
                 script: 'return ["Error: Plugin not properly configured"]'
             ], 
             script: '''
                 def choices = getPromotionChoices()
                 if (choices.contains('build')) {
                     choices.add('BUILD_SOURCE_BRANCH')
                     choices.add('BUILD_DEST_BRANCH')
                 }
                 return choices
             '''
         ]
        ]
    }

    stages {
        stage('Stage-Release') {
            when {
                expression { params.PROMOTION_TYPE == 'stage-release' }
            }
            steps {
                echo "Performing Stage-Release"
                // Add your stage-release steps here
            }
        }

        stage('Build') {
            when {
                expression { params.PROMOTION_TYPE == 'build' }
            }
            steps {
                echo "Performing Build"
                // Add your build steps here
            }
        }
    }
}


