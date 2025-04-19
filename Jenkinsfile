pipeline {
    agent any

    environment {
        AWS_REGION = 'us-east-2'     
        CLUSTER_NAME = 'my-eks-cluster'  
        BRANCH = "${env.BRANCH_NAME}"
    }

    stages {
         stage('Branch Info') {
            steps {
                script {
                    echo "Building branch: ${env.BRANCH_NAME}"
                }
            }
            }
            stage('Deploy Test') {
            when {
                branch 'test'
            }
            steps {
                echo 'Deploying to TEST environment...'
            }
        }
             stage('Deploy main') {
            when {
                branch 'main'
            }
            steps {
                echo 'Deploying to main environment....'
            }
        }
        stage('Configure AWS & Kubeconfig') {
            steps {
                           withCredentials([usernamePassword(credentialsId: 'aws-cr', usernameVariable: 'AWS_ACCESS_KEY_ID', passwordVariable: 'AWS_SECRET_ACCESS_KEY')])  {
    sh 'aws eks update-kubeconfig --name my-eks-cluster'
    sh 'kubectl get pods'
}}
        }
          stage('test') {
            steps {
                                   withCredentials([usernamePassword(credentialsId: 'aws-cr', usernameVariable: 'AWS_ACCESS_KEY_ID', passwordVariable: 'AWS_SECRET_ACCESS_KEY')])  {
    sh 'kubectl get nodes'
}
            }
        }

       
    }
}
