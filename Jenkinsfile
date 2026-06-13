@Library("Shared") _
pipeline{
    agent any
       
    stages {
        stage("Code"){
            steps{
                script {
                clone("https://github.com/Jaimin1010/django-notes-app.git", "main")
            }
            }
        }
        stage('Debug') {
    steps {
        bat 'whoami'
        bat 'docker version'
        bat 'docker info'
    }
}
        stage("Build"){
            steps{
               docker_build("notes-app","latest","jaimin090")
            }
        }
        stage("Push to DockerHub"){
            steps{
                script{
                    docker_push("notes-app","latest","jaimin090")
                }
          }
        }
                stage('Deploy') {
            steps {
                bat "docker compose down -v" 
                bat "docker compose up -d --build"
            }
        }

    }
}
