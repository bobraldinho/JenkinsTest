pipeline {
    agent any

    stages{
        stage('CHECKOUT') {
            steps {
                checkout scm
            }
        }
        stage('BUILD') {
            steps {
                sh 'echo BUILDING STAGE IS COMPLETED'
            }
        }
    } 
}