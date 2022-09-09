pipeline {
    agent any

    stages {
        stage('Hello') {
            steps {
                echo 'Hello World'
            }
        }
		
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
		
		
		
		
    }
	
	

}
