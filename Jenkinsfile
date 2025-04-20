pipeline {
    agent any

    environment {
        REGION = credentials('REGION')
        CLUSTER_NAME = credentials('cluster-name')
        IMAGE_NAME=credentials('image-name')
        AWS_ACCOUNT_ID = credentials('account-id')
        ECR_REPO=credentials('my-ecr-repo')
        
    }

    stages {
        stage('Run Tests') {
    steps {
        script {
            echo "Running unit tests with unittest..."
            sh """
                pip install -r ./application/requirements.txt
                python -m unittest discover -s ./application/test
            """
        }
    }
}
        stage('build and push the image'){
        steps {
        withCredentials([usernamePassword(credentialsId: 'aws-cr', usernameVariable: 'AWS_ACCESS_KEY_ID', passwordVariable: 'AWS_SECRET_ACCESS_KEY')]) {
            script {
              def versionFile = 'version.txt'
                        def currentVersion = readFile(versionFile).trim().toInteger()
                        def newVersion = currentVersion + 1
                        def branchTag = "v${newVersion}"
                        writeFile(file: versionFile, text: "${newVersion}")
                        def fullImageName = "${ECR_REPO}:${branchTag}"
                        env.IMAGE_URI = fullImageName

                        sh """
                            aws ecr get-login-password --region $REGION | docker login --username AWS --password-stdin $ECR_REPO
                            aws ecr get-login-password --region us-east-2 | docker login --username AWS --password-stdin 339712834278.dkr.ecr.us-east-2.amazonaws.com
                            echo "Building Docker image..."
                            docker build -t $IMAGE_NAME -f ./application/Dockerfile ./application
                            echo "Tagging Docker image..."
                            docker tag $IMAGE_NAME:latest $IMAGE_URI
                            echo "Pushing to ECR..."
                            docker push $ECR_REPO:$branchTag
                            echo "Replacing image in deployment.yaml..."
                            sed -i 's|IMAGE_PLACEHOLDER|'"$IMAGE_URI"'|' ./k8s/app-deployment.yml
                        """
            }
        }
        }}
      
        stage('Configure AWS & Kubeconfig') {
            steps {
                 withCredentials([usernamePassword(credentialsId: 'aws-cr', usernameVariable: 'AWS_ACCESS_KEY_ID', passwordVariable: 'AWS_SECRET_ACCESS_KEY')]) {
                 sh 'aws eks update-kubeconfig --name my-eks-cluster --region us-east-2'
                 sh 'kubectl apply -f ./k8s/namespace.yml'
                }
                  
                
            }
        }

        stage('Deploy to TEST') {
        when {
                branch 'test'
            }
            steps {
                withCredentials([usernamePassword(credentialsId: 'aws-cr', usernameVariable: 'AWS_ACCESS_KEY_ID', passwordVariable: 'AWS_SECRET_ACCESS_KEY')]){
                script {
                    def namespace = 'test'
                    echo "Deploying to TEST environment with namespace: $namespace"
                    sh """
                        sed -i 's|NAMESPACE_PLACEHOLDER|$namespace|' ./k8s/configmap.yml
                        sed -i 's|NAMESPACE_PLACEHOLDER|$namespace|' ./k8s/app-deployment.yml
                        sed -i 's|NAMESPACE_PLACEHOLDER|$namespace|' ./k8s/service.yaml
                        kubectl apply -f ./k8s/configmap.yml
                        kubectl apply -f ./k8s/service.yaml
                        kubectl apply -f ./k8s/app-deployment.yml
                    """
                }}
            }
        }

        stage('Deploy to MAIN') {
          when {
                branch 'main'
            }
            steps {
                withCredentials([usernamePassword(credentialsId: 'aws-cr', usernameVariable: 'AWS_ACCESS_KEY_ID', passwordVariable: 'AWS_SECRET_ACCESS_KEY')]){
                script {
                    def namespace = 'prod'
                    echo "Deploying to MAIN environment with namespace: $namespace"
                    sh """
                        sed -i 's|NAMESPACE_PLACEHOLDER|$namespace|' ./k8s/configmap.yml
                        sed -i 's|NAMESPACE_PLACEHOLDER|$namespace|' ./k8s/app-deployment.yml
                        sed -i 's|NAMESPACE_PLACEHOLDER|$namespace|' ./k8s/service.yaml
                        kubectl apply -f ./k8s/configmap.yml
                        kubectl apply -f ./k8s/service.yaml
                        kubectl apply -f ./k8s/app-deployment.yml
                    """
                }}
            }
        }

     

   
    }
}
