

pipeline {
    agent any
    
    stages {
        
        stage ('Git-Pull') {
            steps {
                git branch: 'devops', url: 'https://github.com/diwakarfoujdar/eks-deployment.git'
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
        stage ("Deploy to EKS") {
            steps {
                script {
                    // This unsets the variables that cause the Jenkins HTML error
                    withEnv(["KUBERNETES_SERVICE_HOST=", "KUBERNETES_SERVICE_PORT="]) {
                        sh '''
                        # 1. Update context with your REAL cluster name
                        aws eks update-kubeconfig --region us-east-1 --name b34-cluster
                        
                        # 2. Apply your manifests from the simple-deploy folder
                        kubectl apply -f simple-deploy/
                        
                        # 3. Check if the pods are creating
                        kubectl get pods
                        '''
                    }
                }
            }
        }
        
    }
    
}
