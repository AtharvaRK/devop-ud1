pipeline {
    agent any
   
   environment {
        DOCKER_PASS = credentials('docker_pass')
    } 
 
    stages {
        
        stage('Clean Repo') {
            steps {
                cleanWs()
            }
        }
        
        
        stage('Hello') {
            steps {
                git branch: 'main', credentialsId: 'PAT_Jenkin', url: 'https://github.com/AtharvaRK/devop-ud1'
            }
        }
        
        stage ('Docker Check'){
            steps{
                script{
                    sh 'docker --version'
                    echo 'Login Completed'
                    sh'pwd'
                }
            }
        }
        
        stage ('Docker Login'){
            steps{
                script{
                    withDockerRegistry(credentialsId: 'docker_pass') {
                        sh'docker build -t arkyy21/jenkitbuild:01 .' 
                        sh'docker push arkyy21/jenkitbuild:01'
                        sh'docker rmi arkyy21/jenkitbuild:01'
    
                    }
                }
                
                
            }
        }

        
        
    }
}
