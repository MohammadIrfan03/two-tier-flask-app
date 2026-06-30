pipeline {
    agent { label 'dev' }

    stages {

        stage('Code Checkout') {
            steps {
                git url: "https://github.com/MohammadIrfan03/two-tier-flask-app.git" , branch: "master"
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t my-app .'
            }
        }
        stage('Push to Docker Hub'){
            steps{
                withCredentials([usernamePassword(credentialsId: "dockerHubCreds" , 
                passwordVariable: "dockerHubPass" ,
                usernameVariable: "dockerHubUser"
                )]){
                sh "docker login -u ${env.dockerHubUser} -p ${env.dockerHubPass}"
                sh "docker image tag my-app:latest ${env.dockerHubUser}/two-tier-flask-app"
                sh "docker push ${env.dockerHubUser}/two-tier-flask-app:latest"
                    
                }
            }
        }

        stage('Deploy') {
            steps {
                sh 'docker compose up -d --build'
            }
        }

        stage('Post Deploy') {
            steps {
                echo 'Application is Deployed Successfully....'
            }
        }
    }
}
