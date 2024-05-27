pipeline {
    agent any
    
    environment {
        IMAGE_NAME = 'anupam1897/java-app'
        CONTAINER_NAME = 'java-app'
        PORT_MAPPING = '5000:5000'
        DOCKER_HUB_CREDENTIAL_ID = 'docker-jenkins' // Change as needed, according to your jenkins credentials for dockerhub
    }

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/anupam1897/cit-project.git'
            }
        }

        stage('Retrieve Latest Tag') {
            steps {
                script {
                    def tags = bat(script: 'git tag -l', returnStdout: true).trim().split('\r\n')
                    echo "Tags: ${tags}"
                    latestTag = tags.sort().last()
                    echo "Latest Tag: ${latestTag}"
                    env.TAG = "${latestTag}"
                }
            }
        }
        
        stage('Docker build'){
            steps{
                script{
                powershell "docker build -t '${IMAGE_NAME}-${TAG}:${BUILD_NUMBER}' ."
                }
            }
        }
        
        stage('Run Docker Container') {
            steps {
                script {
                    powershell "docker run -d --name '${CONTAINER_NAME}-${TAG}-${BUILD_NUMBER}'  -p '${PORT_MAPPING}' '${IMAGE_NAME}-${TAG}:${BUILD_NUMBER}'"
                }
            }
        }
        
        stage('Push Docker Image') {
            steps {
                script {
                    try {
                        docker.withRegistry('https://index.docker.io/v1/', "${DOCKER_HUB_CREDENTIAL_ID}") {
                            def image = docker.image("${IMAGE_NAME}-${TAG}:${BUILD_NUMBER}")
                            image.push()
                        }
                    } catch (Exception e) {
                        echo "Error occurred while pushing Docker image: ${e.message}"
                        // You can add additional error handling here if needed
                    }
                }
            }
        }
        
    }

    post {
        always {
            // Clean up workspace after the build
            cleanWs()
        }
        success {
            // Notify success
            // If required connect logging and reporting
            echo 'Build Successful'
        }
            
        failure {
            // Notify failure
            // If required connect logging and reporting
            echo 'Build failed.'
        }
    }
}
