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
               
                sh 'docker build -t raniaboughanmim/virtualization:1.3  .'
            }
        }


        
        stage('Push Image'){
            steps{
                script{
                    withCredentials([string(credentialsId: 'docker_hub_id', variable: 'docker_hub_pwd')]) {
                        sh ' docker login -u raniaboughanmim -p ${docker_hub_pwd}'
                        sh ' docker tag devopsjenkins:latest  raniaboughanmim/virtualization:1.3'
                        sh'docker push  raniaboughanmim/virtualization:1.3 '

}
                }
            }
        }
       
      
        }

    }