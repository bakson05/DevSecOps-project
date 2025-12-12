pipeline {
    agent any
    tools {
        maven 'Maven' 
    }
    stages {
        stage('Example') {
            steps {
                sh 'mvn --version'
            }
        }
    }
}
