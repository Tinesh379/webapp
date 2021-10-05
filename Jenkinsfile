pipeline{
    agent{bode{label'buildfarm'}}
    stages{
        stage('Clone Repo')
        {
            sh 'git clone"https://github.com/Tinesh379/webapp.git"'
            sh 'ls -altr'
        }
        stage('Build'){
            sh 'mvn clean install'
            
        }
    }
      post{
        always{
            cleanWs()
        }
      }
    
    }
}