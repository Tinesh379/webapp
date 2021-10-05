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
        
    }
    post{
        always{
            cleanWs()
        }
    }
}
