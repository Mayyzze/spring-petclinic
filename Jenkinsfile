@Library('sastScaScan') _
properties([
    parameters([
        [$class: 'ChoiceParameter', 
            choiceType: 'PT_SINGLE_SELECT', 
            description: 'Select the Fortify Version Method from the Dropdown List', 
            filterLength: 1, 
            filterable: false, 
            name: 'FortifyVersion', 
            randomName: 'choice-parameter-1', 
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
        ], 
        [$class: 'CascadeChoiceParameter', 
            choiceType: 'PT_SINGLE_SELECT', 
            description: 'Select the Branches from the Dropdown List', 
            filterLength: 1, 
            filterable: false, 
            name: 'Branch', 
            randomName: 'choice-parameter-2', 
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
      stage ("Example") {
        steps {
         script{
          echo 'Hello'
          echo "${params.FortifyVersion}"
          echo "${params.Branch}"
          if (params.Branch.equals("Could not get Environment from Env Param")) {
              echo "Must be the first build after Pipeline deployment.  Aborting the build"
              currentBuild.result = 'ABORTED'
              return
          }
          echo "Crossed param validation"
        } }
      }
  }
}