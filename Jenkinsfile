pipeline {
    agent any
   
   environment {
        DOCKER_PASS = credentials('docker_pass')
    } 
    
    parameters {
        string(name: 'Github_url', defaultValue: 'https://github.com/AtharvaRK/devop-ud1', description: 'Github URL')
        string(name: 'img_tag', defaultValue: '01', description: 'Provide tag of Image')
        string(name: 'img_name', defaultValue: 'jenkitbuild', description: 'Image name')
    }
  
 
    stages {
        
        stage('Clean Repo') {
            steps {
                cleanWs()
            }
        }
        
        
        stage('Hello') {
            steps {
                git branch: 'main', credentialsId: 'PAT_Jenkin', url: "${params.Github_url}"
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
                        sh'docker build -t arkyy21/${img_name}:${img_tag} .' 
                        sh'docker push arkyy21/${img_name}:${img_tag}'
                        sh'docker rmi arkyy21/${img_name}:${img_tag}'
    
                    }
                }
                
                
            }
        }

        
        
    }
}