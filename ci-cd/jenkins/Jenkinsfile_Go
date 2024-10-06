pipeline {
    agent { docker { image 'golang:1.23.2-alpine3.20' } }
    stages {
        stage('build') {
            steps {
                sh 'go version'
            }
        }
    }
}