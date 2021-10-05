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
                sh 'ls -altr'
                sh 'cd webapp'
                sh 'mvn clean package'
            }
        }
        stage('Junit'){
            steps{
                sh "mvn test"
            }
        }
        stage('Deployment'){
            steps{

                deploy adapters: [tomcat9(credentialsId: 'tomcat-manager', path: '', url: 'http://192.168.1.101:8080')], contextPath: null, war: 'target/*.war'
            }
        }
        stage('Deploy to Nexus'){
            steps{
                nexusArtifactUploader artifacts: [[artifactId: '${POM_ARTIFACTID}', classifier: '', file: 'target/{POM_ARTIFACTID}.{POM_PACKAGING}', type: '{POM_PACKAGING}']], credentialsId: 'nexus', groupId: '${POM_GROUPID}', nexusUrl: 'localhost:8081', nexusVersion: 'nexus3', protocol: 'http', repository: 'webapp-snapshots', version: '${POM_VERSION}'
            }
        }
        
        
    }
    post{
        always{
            cleanWs()
        }
    }
}
