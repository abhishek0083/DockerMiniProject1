pipeline {
    agent any
    tools {
        jdk 'OpenJDK11'
        maven 'Maven3'
    }

    stages {
        stage('SCM') {
            steps {
                git changelog: false, poll: false, url: 'https://github.com/abhishek0083/DevopsMiniProject2.git'
            }
        }
        stage('Maven Build') {
            steps {
                echo 'Running Maven build...'
                // Execute Maven build
                bat 'mvn clean install'  // Use 'sh' if on Linux/Mac
            }
        }
        stage('Docker Build & Push') {
            steps {
                script {
                    withDockerRegistry(credentialsId: 'aa12fd4c-6a73-43a6-82d3-5f917a65e9bd') {
                        // Build the Docker image
                        bat "docker build -t abhishek0083/abhi:tag123 ."
                        // Push the Docker image to Docker Hub
                        bat "docker push abhishek0083/abhi:tag123"
                    }
                }
            }
        }
    }
}
