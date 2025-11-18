pipeline {
    agent any

    environment {
        TAG         = "latest"
        REGISTRY    = "${env.REGISTRY_URL}"

        IMAGE_WEB   = "${env.IMAGE_WEB}:${TAG}"
        IMAGE_DB    = "${env.IMAGE_DB}:${TAG}"
        IMAGE_NGINX = "${env.IMAGE_NGINX}:${TAG}"

        COMPOSE_FILE = "${env.COMPOSE_FILE}"

    }

    stages {

        stage('Checkout') {
            steps {
                sh 'echo "Checking out repository..."'
                checkout scm
		slackSend channel: '#devops', message: "Checkout iniciado", tokenCredentialId: 'slack-token'
            }
        }


	stage('Build Images') {
            steps {
                slackSend channel: '#devops', message: "Build das imagens iniciado", tokenCredentialId: 'slack-token'

                script {
                    docker.withRegistry("https://${REGISTRY}", 'dockerhub') {
                        docker.build(IMAGE_WEB,   "-f Dockerfileweb .").push()
                        docker.build(IMAGE_DB,    "-f Dockerfiledb .").push()
                        docker.build(IMAGE_NGINX, "-f Dockerfilenginx .").push()
                    }
                }
            }
        }




    }   
}
