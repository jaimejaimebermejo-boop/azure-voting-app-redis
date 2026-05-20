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
        stage('Docker Push') {
            steps {
                echo "Running in $WORKSPACE"
                dir("$WORKSPACE/azure-vote") {
                    script {
                        docker.withRegistry('', 'dockerhub') {
                            def image = docker.build("jbdelpozo2/jenkins-course:latest")
                            image.push()
                        }
                    }
                }
            }
        }
        stage('Container Scanning') {
            parallel {
                stage('Run Grype') {
                    steps {
                        grypeScan scanDest: 'registry:jbdelpozo2/jenkins-course:latest',
                            repName: 'grype-report.csv',
                            autoInstall: true
                    }
                    post {
                        always {
                            recordIssues(tools: [grype(pattern: 'grype-report.csv')])
                        }
                    }
                }
                stage('Additional Scan') {
                    steps {
                        sleep 10
                        echo 'Additional scan complete'
                    }
                }
            }
        }
    }
}
