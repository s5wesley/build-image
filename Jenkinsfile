pipeline {
    agent any

    environment {
        DOCKER_REGISTRY = 'docker.io'
        DOCKER_IMAGE_NAME = 'nginx'
        DOCKER_IMAGE_TAG = '2'
        DOCKER_REPO_USERNAME = 'mbargabella'
        DOCKER_REPO_PASSWORD = 'dckr_pat_VTa3FXQui2g2gO3rucO1xK1IZ3A'
    }

    stages {
        stage('Clone') {
            steps {
                checkout scm
            }
        }

        stage('Build and Push Docker Image') {
            steps {
                script {
                    // Pull the Nginx image
                    docker.image("${DOCKER_REGISTRY}/${DOCKER_IMAGE_NAME}:${DOCKER_IMAGE_TAG}").pull()

                    // Build the Docker image
                    def customImage = docker.build("${DOCKER_REGISTRY}/${DOCKER_REPO_USERNAME}/${DOCKER_IMAGE_NAME}:${DOCKER_IMAGE_TAG}", ".")

                    // Push the Docker image to the repository
                    customImage.withRegistry("${DOCKER_REGISTRY}", "${DOCKER_REPO_USERNAME}", "${DOCKER_REPO_PASSWORD}") {
                        customImage.push()
                    }
                }
            }
        }
    }
}
