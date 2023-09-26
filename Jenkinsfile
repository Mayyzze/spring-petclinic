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
                withCredentials([secretText(credentialsId: 'sonarToken', secretVariable: 'token')]) {
                // the code here can access $pass and $user
                    echo "SONAR SECRET IS $token"
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