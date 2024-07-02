pipeline {
    agent any
    
    tools{
        jdk 'jdk17'
    }
    
    environment {
        SCANNER_HOME= tool 'sonar-scanner'
    }

    stages {
        stage('Git Checkout') {
            steps {
               git 'https://github.com/syash7202/skmz-app-cd-cd.git'
            }
        }
        

        
        stage('Trivy FS Scan') {
            steps {
                sh "trivy fs ."
            }
        }
        
        stage('Sonarqube Analysis') {
            steps {
                withSonarQubeEnv('sonar') {
                    sh ''' $SCANNER_HOME/bin/sonar-scanner -Dsonar.projectName=SKMZ -Dsonar.projectKey=SKMZ '''
                }
            }
        }
        
        stage('Docker compose') {
            steps {
               sh 'docker compose up -d'
            }
        }  
    }
}
