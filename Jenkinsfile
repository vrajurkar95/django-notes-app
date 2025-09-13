@Library("Shared") _
pipeline {
    
    agent {label "master"}

    stages {
        stage("Init") {
            steps {
                script {
                    hello()   // Must exist in your Shared Library
                }
            }
        }
        stage("checking out code") {
            steps {
              script{
                clone("https://github.com/vrajurkar95/django-notes-app.git","main")
              }
            }
        }

        stage("Build the code") {
            steps {
                script{
                    docker_build("notes-app","latest","842108")
                }
            }
        }

        stage("Push the code") {
            steps {
                script{
                    docker_push("notes-app","latest","842108")
                }
            }
        }

        stage("Deploy the code") {
            steps {
                echo "Deploying with Docker Compose"
                sh "docker compose up -d"
            }
        }
    }
}
