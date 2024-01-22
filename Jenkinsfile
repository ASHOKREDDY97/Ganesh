pipeline {
    environment {
        imagename = "ganeshpoloju/jenkins"
        registryCredential ='dckr_pat_AKkiQ72FXPmBbSyNKYDNMuUX1D4'
        dockerImage = ''
    }
 
    agent any
 
    stages {
        stage('Cloning Git') {
            steps {
                git([url: 'https://github.com/GANESH0369/jenkins.git', branch: 'main'])
            }
        }
 
        stage('Building image') {
            steps {
                script {
                    dockerImage = docker.build "${imagename}:latest"
                }
            }
        }
 
        stage('Running image') {
            steps {
                script {
                    sh "docker run ${imagename}:latest"
                }
            }
        }
 
        stage('Deploy Image') {
            steps {
                script {
                    docker.withRegistry('https://index.docker.io/v1/', registryCredential) {
                        dockerImage.push('latest')
                    }
                }
            }
        }
    }
}
