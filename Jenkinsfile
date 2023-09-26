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

        stage('SAST : Maven Build and SonarQube analysis') {
            when {
                branch "develop"
            }
            steps {
                withCredentials([string(credentialsId: 'sonarToken', variable: 'token')]) {
                    sh "mvn clean install sonar:sonar -Dcheckstyle.skip -Dsonar.token=${token} -Dsonar.host.url=http://172.17.0.1:9000"
                }
            }
        }

        stage('SCA : OWASP Dependency-Check Vulnerabilities') { 
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
                    tag "*"
                }
            }
            steps {
                echo "I have detected the tag"
            }
        }
    }
}