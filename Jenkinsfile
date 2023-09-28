@Library('sastScaScan') _
properties([
    parameters([
        [$class: 'ChoiceParameter', 
            choiceType: 'PT_SINGLE_SELECT', 
            description: 'Select the Fortify Version Method from the Dropdown List', 
            filterLength: 1, 
            filterable: false, 
            name: 'FortifyVersion', 
            script: [
                $class: 'GroovyScript', 
                fallbackScript: [
                    classpath: [], 
                    sandbox: false, 
                    script: 
                        'return[\'Could not get Fortify Version method\']'
                ], 
                script: [
                    classpath: [], 
                    sandbox: false, 
                    script: 
                        'return["stage-release","build"]'
                ]
            ]
            defaultValue: 'stage-release'
        ], 
        [$class: 'CascadeChoiceParameter', 
            choiceType: 'PT_SINGLE_SELECT', 
            description: 'Select the Branches from the Dropdown List', 
            filterLength: 1, 
            filterable: false, 
            name: 'Branch', 
            referencedParameters: 'FortifyVersion', 
            script: [
                $class: 'GroovyScript', 
                fallbackScript: [
                    classpath: [], 
                    sandbox: false, 
                    script: 
                        'return[\'Could not get Fortify Version method from FortifyVersion Param\']'
                ], 
                script: [
                    classpath: [], 
                    sandbox: false, 
                    script: 
                        ''' if (FortifyVersion.equals("stage-release")){
                                return["source-branch"]
                            }
                            else if(FortifyVersion.equals("build")){
                                return["source-branch","dest-branch"]
                            }
                        '''
                ]
            ]
        ]
    ])
])

pipeline {
    environment {
            vari = ""
    }
    
    agent any
    
    stages {
        stage('Stage-Release') {
            when {
                expression { params.FortifyVersion == 'stage-release' }
            }
            steps {
                echo "Performing Stage-Release"
                echo "Selected Branch: ${params.Branch}"
            }
        }

        stage('Build') {
            when {
                expression { params.FortifyVersion == 'build' }
            }
            steps {
                echo "Performing Build"
                echo "Selected Branch: ${params.Branch}"
            }
        }
    }
}