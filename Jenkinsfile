pipeline {
    agent any

    stages {
        stage('pull') {
            steps {
                git branch: 'main', url: 'https://github.com/SanjayTomar22/devops-b34.git'
            }
        }
        stage('PLAN') {
            steps {
               sh '''terraform init
                     terraform plan'''
            }
        }
        stage('APPROVE') {
            steps {
                timeout(10) {
                    input message: 'ALL GOOD?' , ok: "Approve"
                }               
            }
        }
        stage('APPLY') {
            steps {
              sh 'terraform apply --auto-approve'
            }
        }
        stage('deploy') {
            steps {
               sh 'echo "Deploy success"'
            }
        }
    }
}
        
      
