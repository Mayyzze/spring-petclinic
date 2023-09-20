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
        stage('Branch Develop') { 
            when {
                branch "develop"
            }

            steps { 
                sh './mvnw clean package'
                sh 'mvn verify'
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
    }
}