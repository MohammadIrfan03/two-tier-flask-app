pipeline{
    agent any;
    
    stages{
        stage('Code Checkout'){
            steps{
                git 'https://github.com/MohammadIrfan03/two-tier-flask-app.git'
            }
        }
        stage('Build'){
            steps{
                script{
                    sh 'docker build -t mohammadirfan123/two-tier:latest .'
                }
            }
        }
        stage('Docker Push'){
            steps{
                script{
                    withDockerRegistry(credentialsId: 'docker-cred') {
                        sh 'docker push mohammadirfan123/two-tier:latest'
                    }
                }
            }
        }
        stage('Deploy'){
            steps{
                script{
                    sh 'docker compose up -d --build'
                }
            }
        }
    }
}
