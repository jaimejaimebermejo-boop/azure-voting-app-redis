pipeline {
     agent {
        label 'docker'
    }
    stages {
        stage('Verify Branch') {
            steps {
                echo "$GIT_BRANCH"
            }
        }
        stage('Docker Build') {
            steps {
                sh 'docker compose build'
            }
        }
    }
}
