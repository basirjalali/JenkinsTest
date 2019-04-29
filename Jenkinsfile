pipeline {
	agent any
	environment {
		dotnet = "C:/Program Files/dotnet/dotnet.exe"
		iputval= ""
	}
    stages {
        stage('Checkout') {
            steps {
				git credentialsId: '2073aa86-7d97-4d54-8262-8e519461d0ba', url: 'https://github.com/basirjalali/JenkinsTest.git'
            }
        }
        stage('Restore Packages') {
            steps {
             echo 'Restore Packages'
            }
        }
        stage('Clean') {
            steps {
                echo "Clean" 
            }
        }
        stage('Build') {
            steps {
                echo 'Build' 
            }
        }
        stage('Pack') {
            steps {
             echo "Pack" 
            }
        }
        stage('Test') {
            steps {
             echo 'Test' 
            }
        }
        stage('Publish') {
            when {
              expression {
                currentBuild.result == null || currentBuild.result == 'SUCCESS' 
              }
            }
            steps {
             echo 'Publish' 
            }
        }
        stage('Deploy') {
            when {
              expression {
                currentBuild.result == null || currentBuild.result == 'SUCCESS' 
              }
            }
            steps {
             echo 'Deploy' 
            }
        }
        stage('Continue') {
            agent none
            steps {
                script {
                    env.OPTION = input message: 'User input required',
                    parameters: [choice(name: 'options', choices: 'one\ntwo', description: 'Choose one of them')]
                }
            }
        }
        stage('Stage-One') {
            when {
              expression {
                return env.OPTION == 'one'
              }
            }
            steps {
             build job: 'JenkinsTest_1', parameters: [[$class: 'StringParameterValue', name: 'strTest1', value: env.OPTION],[$class: 'StringParameterValue', name: 'strTest2', value: env.BUILD_NUMBER]]
            }
        }
        stage('Stage-two') {
            when {
              expression {
                return env.OPTION == 'two'
              }
            }
            steps {
             build job: 'JenkinsTest_2', parameters: [[$class: 'StringParameterValue', name: 'strTest1', value: env.OPTION],[$class: 'StringParameterValue', name: 'strTest2', value: env.BUILD_NUMBER]]
            }
        }
    }
	post {  
         always {  
             echo 'This will always run'  
         }  
         unstable{
             echo 'Unstable'             
         }
         success {  
             echo 'Done'
         }  
         failure {
             echo 'Failed'
         }  
     }  
}
