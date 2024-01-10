pipeline {
  
    agent {
        label 'Ansible-Node'
    }
    
    tools{
    maven "Localmaven"
    }

    triggers{
    pollSCM('* * * * *')
    }

    options{
    timestamps()
    buildDiscarder(logRotator(artifactDaysToKeepStr: '', artifactNumToKeepStr: '5', daysToKeepStr: '', numToKeepStr: '5'))
    }
  
    stages{

      stage('CheckOutCode'){
        steps{
        git branch: 'master', credentialsId: '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', url: 'https://github.com/Kavana1997/maven-web-app.git'
	
      	}
     }
      stage('Build') {
        steps {
            sh 'mvn clean package'
        }
      }
        
      stage('Create Image'){
        steps{
            steps {
              script {
                sh 'ansible-playbook task.yml'
            	}
            }
         }
      }
    }
}
