pipeline {
    agent any
    
    tools {
        maven 'local_maven'
    }
    
    stages{
        stage('Build'){
            steps {
                sh 'mvn clean package'
            }
            post {
                success {
                    echo 'Archiving the artifacts'
                    archiveArtifacts artifacts: '**/target/*.war'
                }
            }
        }

        stage ('Deployments'){
            
                stage ("Deploy to tomcat server"){
                    steps {
                        deploy adapters: [tomcat9(credentialsId: 'tomcat', path: '', url: 'http://54.147.179.251:8080/')], contextPath: null, war: '**/*.war'

                    }
                }
            }
        }
    }
}
