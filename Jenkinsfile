pipeline {
    agent any
    tools {
        maven 'apache-maven-3.9.11' 
    }
    stages {
        stage('Example') {
            steps {
                sh 'mvn --version'
            }
        }
    }
}
