pipeline {
    agent any

    environment {
        AWS_REGION = 'us-east-2'     
        CLUSTER_NAME = 'my-eks-cluster'  
    }

    stages {
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
    sh 'kubectl delete all --all -n prod -n test'
}
            }
        }

       
    }
}
