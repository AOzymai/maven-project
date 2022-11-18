pipeline {
  agent any
  stages {
    stage ('Build') {
      steps {
        sh "mvn clean package"
      }
      post {
        success {
          echo "Archiving..."
          archiveArtifacts artifacts:'**/target/*.war'
        }
      }
    }
    stage ('Deploy to staging') {
      steps {
        echo "Deploy to staging..."
        build job:'deploy_to_staging'
      }
    }
    stage ('Deploy to prod') {
      steps {
        timeout(time:5, unit:'DAYS') {
          input message:'Approve prod deployment'
        }
        echo "Deploy to prod..."
        build job:'deploy_to_staging'
      }
    }
  }
} 
  
