pipeline {
    agent any
    environment {
        DOCKERHUB_CREDENTIALS = credentials('dockerhub')
        
    }


    stages {
        stage('build app'){
            steps{
                checkout([$class: 'GitSCM', branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[credentialsId: 'dockerhub', url: 'https://github.com/Ran-boughanmi/Virtualization.git']]])
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
                    withCredentials([string(credentialsId: 'docker-hub-id', variable: 'dockerhub')]) {
                        sh ' docker login -u raniaboughanmim -p ${dockerhub}'
                        sh'docker push  raniaboughanmim/virtualization:2.3 '

}
                }
            }
        }
       
      
        }

    }