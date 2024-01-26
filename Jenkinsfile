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
        
        stage('Clean Folder') {
            steps {
                cleanWs()
            }
        }
        
        
        stage('Git Checkout') {
            steps {
                git branch: 'main', credentialsId: 'PAT_Jenkin', url: "${params.Github_url}"
            }
        }
        
        stage ('Docker Check'){
            steps{
                script{
                    sh 'docker --version'
                    echo 'Login Completed'
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

        stage('SonarQube Analysis') {
            steps{
                script{
                    def scannerHome = tool 'sonarscanner';
                    withSonarQubeEnv(credentialsId: 'Sonar', installationName: 'sonar_sys'){
                        sh "${scannerHome}/bin/sonar-scanner \
                        -Dsonar.projectKey=Jenk  "
                    }
                
                }
            }
        }

        stage('Clean Folder post Build') {
            steps {
                cleanWs()
            }
        }
        
    }
}
