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
        stage('Image Scan') {
	steps {
	sh ' trivy image --format template --template "@/usr/local/share/trivy/templates/html.tpl" -o report.html bakson05/sprint-boot-app:latest '
	}
}
		stage('Docker Push') {
    steps {
        withCredentials([string(credentialsId: 'Docker_Hub', variable: 'DOCKER_PAT')]) {
            // Connexion à Docker Hub avec le token
            sh 'echo $DOCKER_PAT | docker login -u "cyberops2025@gmail.com" --password-stdin'
            
            // Push des images
            sh 'docker push bakson05/sprint-boot-app:v1.$BUILD_ID'
            sh 'docker push bakson05/sprint-boot-app:latest'
            
            // Supprimer les images locales après push
            sh 'docker rmi bakson05/sprint-boot-app:v1.$BUILD_ID bakson05/sprint-boot-app:latest'
        }
    }
}


    }
}
