pipeline {
    agent any

    environment {
        DOCKER_IMAGE = "ashayalmighty/website-prt-org"
        KUBERNETES_NAMESPACE = "default"
        DEPLOYMENT_NAME = "website-deployment"
    }

    stages {
        stage('Checkout SCM') {
            steps {
                git url: 'https://github.com/ashaytaksande/Website-PRT-ORG.git', branch: 'main'
            }
        }
        stage('Build Docker Image') {
            steps {
                script {
                    docker.build(DOCKER_IMAGE)
                }
            }
        }
        stage('Push Docker Image') {
            steps {
                script {
                    docker.withRegistry('https://index.docker.io/v1/', 'ee7404fc-3b9e-4c50-a6ea-5bc47ef762fb') {
                        docker.image(DOCKER_IMAGE).push('latest')
                    }
                }
            }
        }
     stage('Deploying App to Kubernetes') {
        steps {
            script {
                kubernetesDeploy(configs: "deploymentservice.yml", kubeconfigId: "k8s")
                }
            }
        }
    }
}

