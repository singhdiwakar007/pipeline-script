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
        sh '''
           cd backend
           mvn clean package -DskipTests'''
      }
    } 
    stage('test stage') {
      steps {
        sh '''
           cd backend
           mvn clean verify sonar:sonar \
             -Dsonar.projectKey=my-app \
             -Dsonar.projectName='my-app' \
             -Dsonar.host.url=http://18.234.108.129:9000 \
             -Dsonar.token=sqp_e5dfb49b176babecbfa7fbda1919f7cd6ebd3155'''
  }
    }
  }
}

        
      
