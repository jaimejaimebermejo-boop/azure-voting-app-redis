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
        stage('Start App') {
            steps {
                sh 'docker compose up -d'
            }
        }
        stage('Run Tests') {
    steps {
        sh 'pip install pytest && pytest tests/'
    }
    post {
        success {
            echo 'Tests passed!'
        }
        failure {
            echo 'Tests failed!'
        }
    }
}
    }
    post {
        always {
            sh 'docker compose down'
        }
    }
}
