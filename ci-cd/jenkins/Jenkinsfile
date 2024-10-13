pipeline {
    agent any
    tools {
          go 'go1.22'
    }
    stages {
      stage('Build') {
        steps {
          echo 'BUILD EXECUTION STARTED'
                sh 'go version'
                sh 'go get ./...'
                sh 'docker build . -t shadowshotx/product-go-micro'
        }
      }
      stage('Test') {
        steps {
          sh 'docker run my-flask-app python -m pytest app/tests/'
        }
      }
      stage('Deploy') {
        steps {
          withCredentials([usernamePassword(credentialsId: 'dockerhub', passwordVariable: 'dockerhubPassword', usernameVariable: 'dockerhubUser')]) {
                sh "docker login -u ${env.dockerhubUser} -p ${env.dockerhubPassword}"
                sh 'docker push shadowshotx/product-go-micro'
            }
        }
      }
    }
    post {
      always {
        sh 'docker logout'
      }
    }
}