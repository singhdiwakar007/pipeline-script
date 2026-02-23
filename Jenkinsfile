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
           mvn sonar:sonar \
           -Dsonar.projectKey=my-app \
           -Dsonar.projectName='my-app' \
           -Dsonar.host.url=http://18.234.108.129:9000 \
           -Dsonar.token=sqp_0080b2c50d2042d47bcd4510d4cbde2422b17670'''
  }
    }
  }
}

        
      
