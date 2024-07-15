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
                    docker.withRegistry('https://index.docker.io/v1/', 'ee7404fc-3b9e-4c50-a6ea-5bc47ef762fb') {
                        def customImage = docker.image("ashayalmighty/website-prt-org")
                        customImage.run('-d -p 80:80 ashayalmighty/website-prt-org')
                    }
                }
            }
        }
    }
}
