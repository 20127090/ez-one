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
                sh "docker start node-server || docker run -d --name node-server --publish 8000:8000 20127090/node-docker:latest"
            }
        }
        stage("Test") {
            steps {
                sh "docker exec -it node-server bash"
                sh "curl http://localhost:8000/test"
            }
        }
    }
}