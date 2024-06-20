pipeline {
  agent any

  options {
    ansiColor('xterm')
  }

  parameters {
    string(name: 'ENV', defaultValue: 'prod', description: 'Environment')
    string(name: 'APPNAME', defaultValue: '', description: 'App Name')
  }

  stages {

    stage ('Get KubeConfig') {
      steps {
        sh 'aws eks update-kubeconfig --name ${ENV}-roboshop'
      }
    }

    stage ('Get App Code') {
      steps {
        dir('APP') {
          git branch: 'main', url: 'https://github.com/Revanthsatyam/${APPNAME}'
        }
        dir('CHART') {
          git branch: 'main', url: 'https://github.com/Revanthsatyam/roboshop-helm'
        }
      }
    }

    stage ('Helm Deployment') {
      steps {
//         sh 'helm install ${APPNAME} ./CHART --set component=${APPNAME}'
//         sh 'helm upgrade -i ${APPNAME} ./CHART --set component=${APPNAME}'
        sh 'helm upgradde -i ${APPNAME ./CHART -f APP/helm/${ENV}.yaml'
      }
    }

  }

  post {
    always {
      cleanWs()
    }
  }

}