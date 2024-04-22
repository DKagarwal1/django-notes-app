pipeline{
    agent any
        
        stages
        {
        stage("code")
        {
            steps
            {
                echo "Cloning the code"
                git url:"https://github.com/DKagarwal1/django-notes-app.git", branch: "main"
                
            }
        }
        stage("build")
        {
            steps
            {
                echo"building the codeby creating pipeline"
                sh "docker build -t django-notes-app ."
            }
            
        }
    stage("Push to Docker Hub"){
            steps {
                echo "Pushing the image to docker hub"
                withCredentials([usernamePassword(credentialsId:"dockerhub",passwordVariable:"dockerHubPass",usernameVariable:"dockerHubUser")]){
                sh "docker tag django-notes-app ${env.dockerHubUser}/django-notes-app:latest"
                sh "docker login -u ${env.dockerHubUser} -p ${env.dockerHubPass}"
                sh "docker push ${env.dockerHubUser}/django-notes-app:latest"
                }
            }
        }
        stage("deploy")
        {
            steps
            {
                echo "deploying the container"
                sh "docker-compose down && docker-compose up -d"

            }
            
        }
    }
}
