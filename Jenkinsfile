pipeline {
    agent any
    environment {
        artifactory_url = '10.0.1.200:8081'
        target = 'spring-boot-tests/spring-boot-smoke-tests/spring-boot-smoke-test-web-ui'
    }
    stages {
        stage ('Maven build') {
            steps {
                
                sh """
                    mvn clean install -f ${target}/pom.xml \
                    -Dmaven.test.skip=true
                """   
            }
        }
        stage ('Archive Artifact') {
            steps {
                archiveArtifacts artifacts: "${target}/target/*.jar"
            }
        }
    }
}
