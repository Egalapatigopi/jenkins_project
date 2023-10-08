pipeline {
    
    agent any 
    
    environment {
        IMAGE_TAG = "${BUILD_NUMBER}"
    }
    
    stages {
        
        stage('Checkout'){
           steps {
                git credentialsId: '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', 
                url: 'https://github.com/Egalapatigopi/jenkins_project',
                branch: 'main'
           }
        }

        stage('Build Docker'){
            steps{
                script{
                    sh '''
                    echo 'Buid Docker Image'
                    docker build -t gopi1998/todoapp:${BUILD_NUMBER} .
                    '''
                }
            }
        }

        stage('Push the artifacts'){
           steps{
                script{
                    sh '''
                    echo 'Push to Repo'
                    docker push gopi1998/todoapp:${BUILD_NUMBER}
                    '''
                }
            }
        }
        
        stage('deploy'){
            steps {
               withDockerRegistry(credentialsId: '3f215577-cdcb-4163-86dd-e7522806a8f6', url: 'https://hub.docker.com/repository/docker/gopi1998/todoapp/general')
               sh '''
               echo 'doplying code to docker-compose'
               
            }
        }
        
    }
}