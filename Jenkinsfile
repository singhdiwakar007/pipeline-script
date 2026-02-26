pipeline {
    agent any

    parameters {
        // This adds the dropdown menu to your Jenkins job
        choice(name: 'ACTION', choices: ['apply', 'destroy'], description: 'Select apply to create or destroy to remove resources')
    }

    stages {
        stage('Pull') {
            steps {
                git branch: 'main', url: 'https://github.com/singhdiwakar007/terraform-eks-infra.git'
            }
        }

        stage('Terraform Init') {
            steps {
                sh 'terraform init'
            }
        }

        stage('PLAN') {
            steps {
                // Shows what will happen based on your choice
                script {
                    if (params.ACTION == 'apply') {
                        sh 'terraform plan'
                    } else {
                        sh 'terraform plan -destroy'
                    }
                }
            }
        }

        stage('APPROVE') {
            steps {
                // Pipeline will pause here for 10 minutes for your confirmation
                timeout(time: 10, unit: 'MINUTES') {
                    input message: "Are you sure you want to ${params.ACTION}?", ok: "Proceed"
                }
            }
        }

        stage('Terraform Action') {
            steps {
                script {
                    if (params.ACTION == 'apply') {
                        echo "🚀 Executing Terraform Apply..."
                        sh 'terraform apply --auto-approve'
                    } else {
                        echo "⚠️ Executing Terraform Destroy..."
                        sh 'terraform destroy --auto-approve'
                    }
                }
            }
        }

        stage('Deploy/Finish') {
            steps {
                script {
                    if (params.ACTION == 'apply') {
                        sh 'echo "EKS Cluster Deploy Success"'
                    } else {
                        sh 'echo "EKS Cluster Destroy Success"'
                    }
                }
            }
        }
    }
}
