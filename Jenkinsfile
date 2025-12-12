pipeline {
    agent any
    
    tools {
        maven 'Maven'
    }
    
    stages {
        stage('Git Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/bakson05/DevSecOps-project.git'
            }
        }
        
        stage('Build & JUnit Test') {
            steps {
                sh 'mvn clean install'
                junit '**/target/surefire-reports/*.xml'
            }
        }
    }
}
