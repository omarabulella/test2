pipeline {
    agent any

    environment {
        AWS_REGION = 'us-east-2'
        CLUSTER_NAME = 'my-eks-cluster'
    }

    stages {
        stage('Show Branch Info') {
            steps {
                echo "Current branch is: ${env.BRANCH_NAME}"
            }
        }

        stage('Deploy to TEST') {
            when {
                branch 'test'
            }
            steps {
                echo 'Deploying to TEST environment...'
            }
        }

        stage('Deploy to MAIN') {
            when {
                branch 'main'
            }
            steps {
                echo 'Deploying to MAIN environment...'
            }
        }

        stage('Configure AWS & Kubeconfig') {
            steps {
                withCredentials([usernamePassword(credentialsId: 'aws-cr', usernameVariable: 'AWS_ACCESS_KEY_ID', passwordVariable: 'AWS_SECRET_ACCESS_KEY')]) {
                    sh 'aws eks update-kubeconfig --name my-eks-cluster --region us-east-2'
                    sh 'kubectl get pods'
                }
            }
        }

        stage('Test K8s Connection') {
            steps {
                withCredentials([usernamePassword(credentialsId: 'aws-cr', usernameVariable: 'AWS_ACCESS_KEY_ID', passwordVariable: 'AWS_SECRET_ACCESS_KEY')]) {
                    sh 'kubectl get nodes'
                }
            }
        }
    }
}
