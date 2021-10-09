@Library('shared-library) _

pipeline{
    agent{node{label 'buildfarm'}}
    stages{
        stage('Git Checkout'){
            steps{
            sh 'git clone "https://github.com/Tinesh379/webapp.git"'
            }
        }
        stage('Build'){
            steps{
                
                mavenGoals()
            }
        }
        stage('Junit'){
            steps{
                sh "mvn test"
            }
        }
        
        stage('Deploy to Nexus'){
            steps{
                script{
                    pom = readMavenPom file: "pom.xml"
                     nexusArtifactUploader(
                            nexusVersion: "nexus3",
                            protocol: "http",
                            nexusUrl: "192.168.1.101:8081",
                            groupId: pom.groupId,
                            version: pom.version,
                            repository: "webapp-releases",
                            credentialsId: "nexus",
                            artifacts: [
                                // Artifact generated such as .jar, .ear and .war files.
                                [artifactId: pom.artifactId,
                                classifier: '',
                                 file: "target/webapp.war",
                                type: pom.packaging],

                                // Lets upload the pom.xml file for additional information for Transitive dependencies
                                [artifactId: pom.artifactId,
                                classifier: '',
                                file: "pom.xml",
                                type: "pom"]
                            ]
                        );

                    }  
            }  
        }
        
    }
    post{
        always{
            cleanWs()
        }
    }
}
