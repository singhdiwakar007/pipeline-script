

pipeline {
    agent any
    
    stages {
        
        stage ('Git-Pull') {
            steps {
                git branch: 'devops', url: 'https://github.com/SanjayTomar22/EasyCRUD.git'
            }
        }
         stage ("Docker--Backend-Build") {
            steps {
                sh '''
                cd backend
                docker build -t kubesanjay/easy-backend:latest .'''
            }
        }
        stage ("Docker-Frontend-Build") {
            steps {
                sh '''
                pwd
                cd frontend
                docker build -t kubesanjay/easy-frontend:latest .'''
            }
        }
         stage ("Docker-Push") {
            steps {
               sh '''
                docker push kubesanjay/easy-backend:latest
                docker push kubesanjay/easy-frontend:latest '''
            }
        }
         stage ("Deploy") {
            steps {
                sh 'kubectl apply -f simple-deploy/. '
            }
        }
        
    }
    
}
