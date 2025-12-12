pipeline {
    agent any
    tools { 
        maven 'Maven' 
    }
    stages {
        stage('Checkout git') {
            steps {
               git branch: 'main', url: 'https://github.com/bakson05/DevSecOps-project.git'
            }
        }
    }
}
stage ('Build & JUnit Test') {
	steps {
		sh 'mvn install' 
	}
	post {
	    success {
		   junit 'target/surefire-reports/**/*.xml'
		} 
	}
}
