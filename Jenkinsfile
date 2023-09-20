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
                echo 'Hello from develop branch'
            }
        }
        stage('Branch Feature') { 
            when {
                branch "feature"
            }

            steps {
                echo 'Hello from feature branch'
            }
        }
    }
}