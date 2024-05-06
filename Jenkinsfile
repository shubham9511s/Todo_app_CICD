  pipeline {
    agent any
   
    stages {
        stage('git-checkout') {
            steps {
               git branch: 'main', changelog: false, poll: false, url: 'https://github.com/shubham9511s/Todo_app_CICD.git'
            }
        }

 
         stage('Docker Build & push') {
            steps {
               script{
                   withDockerRegistry(credentialsId: 'dockerhub') {
                        sh"docker bulid -t todo_app:latest -f backend/Dockerfile ."
                        sh"docker tag todo_app:latest shubhamshinde2025/todo_app:latest"
		        sh"docker push shubhamshinde2025/todo_app:latest"
                    }
               }
            }
        }   
		stage('Deploy to Docker') {
            steps {
               script{
                     withDockerRegistry(credentialsId: 'dockerhub') {
                      sh"docker run -d --name todo_app -p 4000:4000 shubhamshinde2025/todo_app:latest "
                    
                }
               }
            }
        }
        

    }
}
