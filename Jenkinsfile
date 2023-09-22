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
        stage ('Tag detection')
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