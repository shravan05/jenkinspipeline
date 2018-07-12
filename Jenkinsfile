pipeline {
    agent any

    stages{
        stage('Build'){
            steps {
                sh 'mvn clean package'
            }
            post {
                success {
                    echo 'Now Archiving...'
                    archiveArtifacts artifacts: '**/target/*.war'
                }
            }
        }
        stage ('Deploy to Dev'){
            steps {
                build job: 'pipeline-deploy-to-dev'
            }
        }
    }
}
