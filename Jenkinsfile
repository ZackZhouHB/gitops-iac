pipeline {
    agent {
        kubernetes {
            label 'jenkins=true' // Label of the Kubernetes slave node
            defaultContainer 'jnlp'
        }
    environment {
        DOCKER_IMAGE = 'zackz001/gitops-jekyll'
        KUBE_NAMESPACE = 'zack'
        DEPLOYMENT_NAME = 'zackweb-app'
        GIT_REPO_URL = 'https://github.com/ZackZhouHB/gitops-iac.git'
    }
    
    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: GIT_REPO_URL
            }
        }
        
      
        stage('Deploy to Kubernetes') {
            steps {
                script {
                    kubeConfig = readFile("/home/ubuntu/.kube/config") // Path to your kubeconfig file
                    kubeConfigContent = kubeConfig.readLines().join('\n')
                    withKubeConfig([credentialsId: 'kubeconfig-credentials', kubeconfigContent: kubeConfigContent]) {
                        sh "kubectl apply -f deploy.yaml -n $KUBE_NAMESPACE"
                    }
                }
            }
        }
    }
}
