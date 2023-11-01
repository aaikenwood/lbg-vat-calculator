pipeline {
  agent any
  stages{
    stage('Checkout') {
      steps {
        git branch: 'main', url : 'https://github.com/aaikenwood/lbg-vat-calculator.git'
      }
    }
    stage('Install') {
      steps {
        sh "npm install"
      }
    }
    stage('Test') {
      steps{
        sh "npm test"
      }
    }
    stage('SonarQube Analysis') {
      environment{
        scannerHome = tool 'sonar-cube-aaw2'
      }
      steps {
        withSonarQubeEnv('sonar-qube-1') {
          sh "${scannerHome}/bin/sonar-scanner"
        }
        timeout(time: 10, unit: "MINUTES"){
          waitForQualityGate abortPipeline: true
        }
      }
    }
  }
}
