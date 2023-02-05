pipeline {
    agent {label 'noprojeto'}
    stages {
        stage('Clone repository') { 
            steps {
              git (
                branch: 'main',
                url: 'git@github.com:RenataKB/projeto-final-cicd.git'
              )
            }
        }

        
        stage('Build dev'){
            when {
               not {
                  branch "main"
               }
            }
            steps { 
                script{
                 image = docker.build("renatakb/v1:develop")
                 
                }
            }
        }
        stage('Build') {
            when {
                branch "main"
            } 
            steps { 
                script{
                 image = docker.build("renatakb/v1:main")
                }
            }
        }
        stage('Push') {
            steps {
                script{
                       docker.withRegistry('', 'docker') {
                       image.push()
                    }
                }
            }
        }
    }
}