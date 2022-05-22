pipeline {
    agent any
    environment {
        PATH="/opt/maven/apache-maven-3.8.5/bin:$PATH"
    }
    stages {
        stage('Git') {
            steps {
                git 'https://github.com/vedantguptha/AppLandingpage.git'
            }
        }
         stage('Clean') {
            steps {
                sh "mvn clean"
            }
        }
        stage('Build War File'){
            steps {
                sh "mvn -DskipTests package "
            }
        }
        stage('SSH File Transfer'){
            
            steps{
                sshPublisher(publishers: [sshPublisherDesc(configName: 'dockerhost', transfers: [sshTransfer(cleanRemote: false, excludes: '', execCommand: '', execTimeout: 120000, flatten: false, makeEmptyDirs: false, noDefaultExcludes: false, patternSeparator: '[, ]+', remoteDirectory: '', remoteDirectorySDF: false, removePrefix: 'webapp/target/', sourceFiles: 'webapp/target/*.war')], usePromotionTimestamp: false, useWorkspaceInPromotion: false, verbose: false)])
            }
            
        }
        stage('Buid Docker File'){
            steps{
                sshPublisher(publishers: [sshPublisherDesc(configName: 'dockerhost', transfers: [sshTransfer(cleanRemote: false, excludes: '', execCommand: 'docker build -t webapp:v2 .', execTimeout: 120000, flatten: false, makeEmptyDirs: false, noDefaultExcludes: false, patternSeparator: '[, ]+', remoteDirectory: '', remoteDirectorySDF: false, removePrefix: '', sourceFiles: '')], usePromotionTimestamp: false, useWorkspaceInPromotion: false, verbose: false)])
            }
        }
    }
}
