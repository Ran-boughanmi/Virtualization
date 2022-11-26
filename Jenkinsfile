pipeline {
    agent any
    environment {
        DOCKERHUB_CREDENTIALS = credentials('docker-hub-rania')
        
    }


    stages {
        stage('build app'){
            steps{
                checkout([$class: 'GitSCM', branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[credentialsId: 'docker-hub-rania', url: 'https://github.com/Ran-boughanmi/Virtualization.git']]])
            }
        }
       

        stage('Docker Build') {
            steps {
               
                sh 'docker build -t raniaboughanmim/virtualization:2.1 . '
            }
        }


        
        stage('Push Image'){
            steps{
                script{
                    withCredentials([string(credentialsId: 'docker-hub-id', variable: 'docker-hub-pwd')]) {
                        sh ' docker login -u raniaboughanmim -p ${docker-hub-pwd}'
                        sh'docker push  raniaboughanmim/virtualization:2.3 '

}
                }
            }
        }
       
      
        }

    }