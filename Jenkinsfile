pipeline {
    agent any
    tools {
        maven 'maven-3.9.11' 
    }
    stages {
        stage('Example') {
            steps {
                sh 'mvn --version'
            }
        }
    }
}
