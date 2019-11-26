pipeline {
    agent any
    environment {
        GITHUB_CREDS = credentials('GITHUB_CRED')
    }
    options {
        disableConcurrentBuilds()
        timeout(time: 15, unit: 'MINUTES')
    }
    stages {
        stage('Docker Build') {
          steps {
            sh 'npm install'
            sh 'docker build -t arkanenetwork/arkane-documentation:${BRANCH_NAME} .'
          }
        }
        stage('Docker Push') {
          steps {
            withCredentials([usernamePassword(credentialsId: 'dockerHub', passwordVariable: 'dockerHubPassword', usernameVariable: 'dockerHubUser')]) {
              sh "docker login -u ${env.dockerHubUser} -p ${env.dockerHubPassword}"
              sh "docker push arkanenetwork/arkane-documentation:${BRANCH_NAME} && echo 'pushed'"
            }
          }
        }
    }
}
