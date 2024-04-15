pipeline{
        agent {
                docker {
                image 'maven'
                // args '-v $HOME/.m2:/root/.m2'
                args '-u root'
                }
        }
        stages{
              stage('Sonar Scan'){
                  steps{
                      script{
                      withSonarQubeEnv('sonarserver') { 
                      sh "mvn sonar:sonar"
                       }
		              // sh "mvn clean install"
                  }
                }  
              }
              stage('Maven Build'){
                  steps{
                      script{
		                  sh "mvn clean install"
                  }
                }  
              }
              stage('Deploy'){
                  steps{
		    deploy adapters: [tomcat8(credentialsId: 'Deployer', path: '', url: 'http://13.201.67.201:8080/')], contextPath: 'demo', war: 'target/*.war'	  
                }  
              }
        }
}
