pipeline {
    agent any

    tools { 
        maven 'Maven' 
    }

    stages {

        stage('Checkout Git') {
            steps {
                git branch: 'main',
                    url: 'https://github.com/bakson05/DevSecOps-project.git'
            }
        }

        stage('Build & JUnit Test') {
            steps {
                sh 'mvn clean install'
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
                    sh '''
                        mvn sonar:sonar \
                        -Dsonar.projectKey=DevSecOps-project \
                        -Dsonar.projectName=DevSecOps-project
                    '''
                }
            }
        }
        stage('Docker Build') {
    steps {
        sh 'docker build -t bakson05/sprint-boot-app:v1.$BUILD_ID .'
        sh 'docker image tag bakson05/sprint-boot-app:v1.$BUILD_ID bakson05/sprint-boot-app:latest'
    }
}

    }
}
