pipeline {
    agent any
    environment {
        artifactory_url = '18.217.84.244:8081'
    }
    stages {
        stage ('Maven build') {
            steps {
                
                sh """
                    mvn clean install -f spring-boot-tests/spring-boot-smoke-tests/spring-boot-smoke-test-web-ui/pom.xml \
                    -Dmaven.test.skip=true
                """   
            }
        }
        stage ('Archive Artifact') {
            steps {
                archiveArtifacts artifacts: 'target/*.jar'
            }
        }
    }
}