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
                sh "docker build -t node-docker ."
            }
        }
        stage("Push") {
            steps {
                withDockerRegistry(credentialsId: 'docker', url: 'https://index.docker.io/v1/') {
                    sh "docker push node-docker:latest"
                }
            }
        }
    }
}