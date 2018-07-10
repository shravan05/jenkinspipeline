pipeline {
    agent any
    
    parameters { 
         string(name: 'tomcat_staging', defaultValue: 'localhost', description: 'Staging Server')
         string(name: 'tomcat_prod', defaultValue: 'localhost', description: 'Production Server')
    } 

    triggers {
         pollSCM('* * * * *') // Polling Source Control
     }

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

        stage ('Deployments'){
            parallel{
                stage ('Deploy to Staging'){
                    steps {
                        sh "cp **/target/*.war /var/lib/tomcat-staging/webapps"
                    }
                }

                stage ("Deploy to Production"){
                    steps {
                        sh "cp **/target/*.war /var/lib/tomcat-production/webapps"
                    }
                }
            }
        }
    }
}
