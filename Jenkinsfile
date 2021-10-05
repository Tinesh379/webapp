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
        
    }
    post{
        always{
            cleanWS()
        }
    }
}