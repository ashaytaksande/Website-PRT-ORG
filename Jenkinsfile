pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                script {
                    def app = docker.build("ashayalmighty/website-prt-org")
                }
            }
        }

        stage('Deploy') {
            steps {
                script {
                    def customImage = docker.image("ashayalmighty/website-prt-org")
                    customImage.inside {
                        sh 'docker run -d -p 80:80 ashayalmighty/website-prt-org'
                    }
                }
            }
        }
    }
}
