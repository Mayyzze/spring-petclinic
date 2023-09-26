pipeline { 
    agent any 
    options {
        skipStagesAfterUnstable()
    }
    tools {
        maven "MyMaven"
    }
    stages {
        stage('Hello') { 
            steps { 
                sh 'java -version' 
            }
        }
        stage('Build') {
            when {
                branch "d"
            } 
            steps { 
                sh './mvnw clean install -Dcheckstyle.skip' 
            }
        }
        stage('OWASP Dependency-Check Vulnerabilities') { 
            when {
                branch "d"
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

        stage('SonarQube analysis') {
            steps {
                echo "SONAR SECRET IS ${2701857f-a36c-4d79-ac19-0972af13cddb}"
              }
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
                    tag "*"
                }
            }
            steps {
                echo "I have detected the tag"
            }
        }
    }
}