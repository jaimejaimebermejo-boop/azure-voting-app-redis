@Library('demo-shared-pipeline@master') _

pipeline {
    agent {
        label 'docker'
    }
    stages {
        stage('Call Library Function') {
            steps {
                script {
                    helloWorld()
                }
            }
        }
    }
}
