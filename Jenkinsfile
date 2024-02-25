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
                    kubernetesDeploy(configs: "zackweb.yaml")

                }  
             }
            }
        }
    }
}
