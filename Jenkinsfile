pipeline {
    agent any
    stages {
            when {
        branch 'master'
    }
        stage('Build Docker Image') {
                when {
        branch 'master'
    }

            steps {
                script {
                    app = docker.build("alaazidan/todos_app")
                    app.inside {
                        sh 'echo $(curl localhost:3000)'
                    }
                }
            }
        }
        stage('Push Docker Image') {
                when {
        branch 'master'
        }

            steps {
                script {
                    docker.withRegistry('https://registry.hub.docker.com', 'my_docker_hub_login') {
                        app.push("${env.BUILD_NUMBER}")
                        app.push("latest")
                    }
                }
            }
        }
    }   
}
