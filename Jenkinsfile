

pipeline {
    agent any
    
    stages {
        
        stage ('Git-Pull') {
            steps {
                git branch: 'devops', url: 'https://github.com/singhdiwakar007/eks-deployment.git'
            }
        }
         stage ("Docker--Backend-Build") {
            steps {
                sh '''
                cd backend
                docker build -t diwakar2010/easy-backend . '''
            }
        }
        stage ("Docker-Frontend-Build") {
            steps {
                sh '''
                pwd
                cd frontend
                docker build -t diwakar2010/easy-frontend . '''
            }
        }
         stage ("Docker-Push") {
            steps {
               sh '''
                docker push diwakar2010/easy-backend
                docker push diwakar2010/easy-frontend '''
            }
        }
         stage ("Deploy") {
            steps {
                sh 'kubectl apply -f simple-deploy/. '
            }
        }
        
    }
    
}
