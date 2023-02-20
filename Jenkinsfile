pipeline {
    agent any
    stages {
        stage('MVN Build') {
             steps{
                 echo "Building War File............."
                 sh "mvn clean install"
            }
            post {
                success {
                    echo "Archiving Artifacts"
                    archiveArtifacts artifacts: '**/target/*.war'
                }
            }
        }
        stage('Deploy War To Tomcat Server') { 
            steps {
                deploy adapters: [tomcat7(credentialsId: 'tomcat', path: '', url: 'http://43.204.107.178:8080/')], contextPath: '/opt/tomcat9/webapps', war: '**/*.war'
            }
        }
    }
}
