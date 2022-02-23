pipeline {
    agent any
    stages {
        stage('Pull Code From Git') {
            steps {
                // Get  code from a GitHub repository
                git credentialsId: 'git', url: 'https://github.com/sandevops27/AppLandingpage'
            }

        }
    }
}
