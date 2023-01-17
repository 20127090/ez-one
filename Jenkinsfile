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
    }
}