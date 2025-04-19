pipeline {
    agent any

    environment {
        REGION = 'us-east-2'
        CLUSTER_NAME = 'my-eks-cluster'
        IMAGE_NAME="my-app"
        AWS_ACCOUNT_ID ='339712834278'
        ECR_REPO="339712834278.dkr.ecr.us-east-2.amazonaws.com/myapp"
        
    }

    stages {
        stage('build and push the image'){
        steps {
        withCredentials([usernamePassword(credentialsId: 'aws-cr', usernameVariable: 'AWS_ACCESS_KEY_ID', passwordVariable: 'AWS_SECRET_ACCESS_KEY')]) {
            script {
                def branchTag = env.BRANCH_NAME

                sh """
                  
                    aws ecr get-login-password --region $REGION | docker login --username AWS --password-stdin $ECR_REPO

                    echo "Building Docker image..."
                    docker build -t $IMAGE_NAME -f ./application/Dockerfile ./application

                    echo "Tagging Docker image..."
                    docker tag $IMAGE_NAME:latest $ECR_REPO:$branchTag

                    echo "Pushing to ECR..."
                    docker push $ECR_REPO:$branchTag
                """
            }}
        }}
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
