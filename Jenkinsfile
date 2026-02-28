

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
                script {
                    // This unsets the variables causing the "HTML/Login" error
                    withEnv(["KUBERNETES_SERVICE_HOST=", "KUBERNETES_SERVICE_PORT="]) {
                        sh '''
                        # 1. Refresh the connection to your specific EKS cluster
                        aws eks update-kubeconfig --region us-east-1 --name your-cluster-name
                        
                        # 2. Apply your manifests
                        kubectl apply -f simple-deploy/
                        
                        # 3. Verify the pods are starting
                        kubectl get pods
                        '''
                    }
                }
            }
        }
        
    }
    
}
