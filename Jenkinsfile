pipeline {
  agent any
  stages {
    stage('pull stage') {
      steps {
       git branch: 'main', url: 'https://github.com/shubhamkalsait/EasyCRUD.git'
      }
    }
    stage('build stage') {
      steps {
        sh '''cd backend
        mvn clean package -DskipTests'''
      }
    } 
  }
}
        
      
