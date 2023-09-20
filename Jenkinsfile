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
        stage('Branch') { 
            when {
                branch "develop"
            }

            steps { 
                echo 'Hello from develop branch'
            }

            when {
                branch "feature"
            }

            steps {
                echo 'Hello from feature branch'
            }
        }
    }
}