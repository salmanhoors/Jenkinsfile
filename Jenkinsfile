pipeline {
    agent any

    tools {
        maven 'Maven-3.9.10'
    }

    stages {
        stage('Build') {
            steps {
                sh 'mvn clean package'
            }
            post {
                success {
                    echo "Archiving the Artifacts"
                    archiveArtifacts artifacts: '**/target/*.war'
                }
            }
        }

        stage('Deploy to tomcat server') {
            steps {
                deploy adapters: [
                    tomcat7(
                        credentialsId: 'tomcat_deployer',
                        url: 'http://3.110.115.24:8080/',
                        path: '',
                        alternativeDeploymentContext: ''
                    )
                ],
                contextPath: null,
                war: '**/*.war'
            }
        }
    }
}
