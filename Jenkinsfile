pipeline{
    agent any
       
    stages {
        stage("Code"){
            steps{
                echo "This is cloning the code"
                git url: "https://github.com/Jaimin1010/django-notes-app.git", branch: "main"
                echo "code cloning successful"
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
                echo "This is building the code"
                bat "docker build -t notes-app:latest ."
            }
        }
        stage("Push to DockerHub"){
            steps{
                echo "This is pushing the image to Docker Hub"
              withCredentials([usernamePassword(
    credentialsId: 'dockerHubCred',
    usernameVariable: 'dockerHubUser',
    passwordVariable: 'dockerHubPass'
)]) {

    bat '''
    docker login -u %dockerHubUser% -p %dockerHubPass%
    docker tag notes-app:latest %dockerHubUser%/notes-app:latest
    docker push %dockerHubUser%/notes-app:latest
    '''
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
