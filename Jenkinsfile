pipeline {
    agent any
    stages {
        stage("Clone") {
            steps {
                git credentialsId: 'Git', url: 'https://github.com/20127090/ez-one.git'
            }
        }
        stage("Build") {
            steps {
                sh "docker build -t 20127090/node-docker ."
            }
        }
        stage("Push") {
            steps {
                withDockerRegistry(credentialsId: 'docker', url: 'https://index.docker.io/v1/') {
                    sh "docker push 20127090/node-docker:latest"
                }
            }
        }
        stage("Deploy") {
            steps {
                docker run --publish 8000:8000 node-docker
            }
        }
    }
}