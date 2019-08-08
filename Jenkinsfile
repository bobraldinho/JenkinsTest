pipeline {
    agent any
    environment {
        artifactory_url = '18.217.84.244:8081'
    }
    stages {
        stage ('Maven build') {
            steps {
                
                sh 'mvn clean install -Dmaven.test.skip=true'
                
            }
        }
        stage ('Archive Artifact') {
            steps {
                archiveArtifacts artifacts: 'target/*.jar'
            }
        }
    }
}