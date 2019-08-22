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
        stage ('Uploading to Artifactory') {
            steps {    
                rtUpload (
                    serverId: "artifactory",
                    spec:
                        """{
                          "files": [
                            {
                              "pattern": "target/*jar",
                              "target": "djqyfvbhjd/${BUILD_NUMBER}/"
                            }
                         ]
                        }"""
                )
            }
        }
        stage ('Invoke Ansible deploy playbook') {
            steps {
               sh 'ansible-playbook -i /tmp/inventory tmp/deploy_to_ci.yml -u ubuntu --private-key ~/gradwork.pem -e "artifactory_url=${artifactory_url} build_number=${BUILD_NUMBER}"'
            }
        }
    }
}
