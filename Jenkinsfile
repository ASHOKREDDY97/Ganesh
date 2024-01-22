pipeline {
    environment {
        imagename = "ganeshpoloju/jenkins"
        registryCredential = 'dckr_pat_AKkiQ72FXPmBbSyNKYDNMuUX1D4'
        dockerImage = ''
    }

    agent any

    stages {
        stage('Cloning Git') {
            steps {
                script {
                    git branch: 'main', url: 'https://github.com/GANESH0369/jenkins.git'
                }
            }
        }

        stage('Building image') {
            steps {
                script {
                    dockerImage = docker.build(imagename + ":latest")
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
                    docker.withRegistry('', registryCredential) {
                        dockerImage.push('latest')
                    }
                }
            }
        }
    }
}
