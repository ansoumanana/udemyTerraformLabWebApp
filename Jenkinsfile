pipeline{
    //Directives
    agent any
    tools {
        maven 'maven'
    }
    environment{
        ArtifactId = readMavenPom().getArtifactId()
        Version = readMavenPom().getVersion()
        Name = readMavenPom().getName()
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
                script {
                   def NexusRepo = Version.endsWith("SNAPSHOT") ? "VinaysDevOpsLab-SNAPSHOT" : "VinaysDevOpsLab-RELEASE"
                   nexusArtifactUploader artifacts:
                    [[
                        artifactId: "${ArtifactId}",
                        classifier: '',
                        file: "target/${ArtifactId}-${Version}.war",
                        type: 'war'
                     ]],
                      credentialsId: '4778c691-2333-4159-a2c6-70df66086803',
                      groupId: 'com.vinaysdevopslab',
                      nexusUrl: '172.20.10.210:8081',
                      nexusVersion: 'nexus3',
                      protocol: 'http',
                      repository: "${NexusRepo}",
                      version: "${Version}"
                }

            }
        }

          // Stage 4 : Print some information
        stage ('Print Environment variables'){
            steps {
                echo "Artifact ID is '${ArtifactId}'"
                echo "Version is '${Version}'"
                echo "GroupID is '${GroupId}'"
                echo "Name is '${Name}'"
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