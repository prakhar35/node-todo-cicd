pipeline{
    agent  {label 'dev-2'}
    
    stages{
        stage('Code'){
            steps{
                git url: 'https://github.com/prakhar35/node-todo-cicd.git', branch: 'master'
            }   
        }
        stage('Build and Test'){
            steps{
                sh 'docker build . -t prakhar04/node-todo-app-cicd:latest'
            }   
        }
        stage('Login and Push Image'){
            steps{
                echo 'Logging into docker and pushing code'
                withCredentials([usernamePassword(credentialsId:'dockerHub',
                passwordVariable:'dockerHubPassword',usernameVariable:'dockerHubUser')]) {

                    sh "docker login -u ${env.dockerHubUser} -p ${env.dockerHubPassword}"
                    sh "docker push prakhar04/node-todo-app-cicd:latest"
                }
            }   
        }
        stage('Deploy'){
            steps{
                sh 'docker-compose down && docker-compose up -d'
            }
        }
    }
}
