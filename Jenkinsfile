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
   stage('SonarQube Analysis') {
    steps {
        dir('backend') {
            // 'sonar-server' is the Name you gave in Jenkins System settings
            withSonarQubeEnv('sonar-server') { 
                sh "mvn sonar:sonar -Dsonar.projectKey=my-app"
            }
        }
    }
}
  }
    }

        
      
