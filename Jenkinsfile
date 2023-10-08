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
              sh '''
              docker login
              docker push gopi1998/todoapp:${BUILD_NUMBER}
              '''
            }
        }
        
        stage('deploy'){
            steps {
               sh '''
               docker login
               docker pull gopi1998/todoapp:${BUILD_NUMBER}
               echo 'doplying code to docker-compose'
               docker-compose up -d 
               '''
            }
        }
    }
}
                
