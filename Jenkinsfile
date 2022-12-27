pipeline{
    //Directives
    agent any
    tools {
        maven 'maven'
    }

    stages {
        // Specify various stage with in stages

        // stage 1. Build
        stage ('Build'){
            steps {
                sh 'mvn clean install package'
            }
        }

        // Stage2 : Testing
        stage ('Test'){
            steps {
                echo ' testing......'

            }
        }

        // Stage3 : Publish the source code to Sonarqube
        stage('Publish to nexus'){
            steps{
                nexusArtifactUploader artifacts: [[artifactId: 'VinayDevOpsLab', classifier: '', file: 'target/VinayDevOpsLab-0.1.0-SNAPSHOT.war', type: 'war']], credentialsId: '4778c691-2333-4159-a2c6-70df66086803', groupId: 'com.vinaysdevopslab', nexusUrl: '172.20.10.210:8081', nexusVersion: 'nexus3', protocol: 'http', repository: 'udemyDevopslab-snapshot', version: '0.1.0-SNAPSHOT'
            }
        }
        /*stage ('Sonarqube Analysis'){
            steps {
                echo ' Source code published to Sonarqube for SCA......'
                withSonarQubeEnv('sonarqube'){ // You can override the credential to be used
                     sh 'mvn sonar:sonar'
                }

            }
        }*/

        
        
    }

}