pipeline {

   agent any

   tools{
      maven 'tp premier test'
   }

   stages {
      stage('Clone') {
         steps {
            checkout([$class: 'GitSCM',
                branches: [[name: '*/master' ]],
                extensions: scm.extensions,
                userRemoteConfigs: [[
                    url: 'https://github.com/Pierrelagi/TP2.git',
                    credentialsId: 'e3f5d12c-a699-4196-870d-2112026dfa1b'
                ]]
            ])

            //List all directories
            sh "ls -lart ./*"
         }
      }
	  stage('Compile'){
         steps{
            withMaven(maven:'tp premier test')
            {
              sh "mvn compile"
            }
         }
      }
      stage('Test'){
         steps{
            withMaven(maven:'tp premier test')
            {
              sh "mvn test"
            }
         }
         
      }
      
      stage('Build'){
         steps{
            sh "mvn -B -DskipTests clean install"
         }
      }
	  

	  
	  stage ('SonarQube analysis') {
         steps {
            withSonarQubeEnv(installationName: 'My local Sonar', credentialsId: 'e3f5d12c-a699-4196-870d-2112026dfa1b') {
               sh 'mvn clean sonar:sonar -Dsonar.login=$Login -Dsonar.password=$Password'
            }
         }
      }
      
      
	stage('Code Coverage') {
        steps {
            sh 'mvn clean cobertura:cobertura'
        }
        
        post {
	        always {
	            step([$class: 'CoberturaPublisher', autoUpdateHealth: true, autoUpdateStability: true, coberturaReportFile: '**/target/site/cobertura/*.xml', failUnhealthy: false, failUnstable: false, maxNumberOfBuilds: 2, onlyStable: false, sourceEncoding: 'ASCII', zoomCoverageChart: true])
	        }
	    }
    }

	  
	  
}
}
