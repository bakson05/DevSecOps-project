pipeline {
    agent any

    tools {
        maven 'Maven'
    }

    stages {

        stage('Git Checkout') {
            steps {
                git branch: 'main',
                    url: 'https://github.com/bakson05/DevSecOps-project.git'
            }
        }

        stage('Build & JUnit Test') {
            steps {
                sh 'mvn install'
            }
            post {
                success {
                    junit 'target/surefire-reports/**/*.xml'
                }
            }
        }

        stage('SonarQube Analysis') {
            steps {
                withSonarQubeEnv('SonarQube') {
                    sh 
                        mvn clean verify sonar:sonar \
                        -Dsonar.projectKey=devsecops-project-key \
                        -Dsonar.login=Sonar
                }
            }
        }

    }
}
