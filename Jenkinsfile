pipeline {
    agent {label 'noprojeto'}
    options {
        ansiColor('xterm')
    }
    stages {
        stage('Clone repository') { 
            steps {
              git (
                branch: 'main',
                url: 'https://github.com/RenataKB/projeto-final-cicd.git'
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
                 image = docker.build("grupo2/v1:develop")
                 
                }
            }
        }
        stage('Build') {
            when {
                branch "main"
            } 
            steps { 
                script{
                 image = docker.build("grupo2/v1:main")
                }
            }
        }
        stage('Push') {
            steps {
                script{
                       docker.withRegistry('https://hub.docker.com/', 'dockerhub') {
                       image.push()
                    }
                }
            }
        }
        stage('Not Push') {
            steps {
                echo '\033[34mSorry!\033[0m \033[33mI am not creating\033[0m \033[35ma DockerHub account!\033[0m'
            }
        }
        
//         stage('Deploy') {
//             steps {
//                  script {
//                     docker.image("grupo2/v1:main").withRun('-p 3000:3000') {c ->
//                         sleep 60
//                     }
//                 }
//             }
//         }
    }
}
