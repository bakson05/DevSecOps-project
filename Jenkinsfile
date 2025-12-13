stage('SonarQube Analysis') {
    steps {
        withSonarQubeEnv('SonarQube') {
            sh '''
                mvn clean verify sonar:sonar \
                -Dsonar.projectKey=devsecops \
                -Dsonar.login=Sonar
            '''
        }
    }
}
