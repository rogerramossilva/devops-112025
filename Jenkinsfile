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
            }
        }
    }   
}
