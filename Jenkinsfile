@Library('test-library') _
library identifier: 'test-library@main', retriever: modernSCM(
  [$class: 'GitSCMSource',
   remote: 'https://github.com/Mayyzze/test-library.git'])
pipeline { 
    agent any 
    options {
        skipStagesAfterUnstable()
    }
    stages {
        stage('Hello') { 
            steps { 
                sh 'java -version' 
            }
        }
        stage('Build') {
            when {
                branch "develop"
            } 
            steps { 
                sh './mvnw clean install -Dcheckstyle.skip' 
            }
        }
        stage('OWASP Dependency-Check Vulnerabilities') { 
            when {
                branch "develop"
            }
            steps {
                dependencyCheck additionalArguments: ''' 
                    -o './'
                    -s './'
                    -f 'ALL' 
                    --prettyPrint''', odcInstallation: 'OWASP Dependency-Check Vulnerabilities'
        
                dependencyCheckPublisher pattern: 'dependency-check-report.xml'
            }
        }
        stage('Branch Feature') { 
            when {
                branch "feature*"
            }

            steps {
                echo 'Hello from feature branch'
            }
        }
        stage ('Tag detection') {
            when {
                allOf {
                    branch "feature*"
                    tag "test*"
                }
            }
            steps {
                echo "I have detected the tag 5"
            }
        }
        stage ('Test Library') {
            steps {
                sastScaScan.helloWorld()
            }
        }
    }
}