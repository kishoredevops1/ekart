pipeline {
    agent any
    triggers {
        pollSCM('H/5 * * * 1-5')
    }
    tools {
        maven 'Maven3'
        jdk 'java8'
      
    }
    stages {
      stage('Checkout') {
                steps {
                                checkout scm                           
                }
                    }
        stage ('Initialize') {
            steps {
                sh '''
                    echo "PATH = ${PATH}"
                    echo "M2_HOME = ${M2_HOME}"
                '''
            }
        }

        stage ('Build') {
            steps {
                sh 'mvn -Dmaven.test.failure.ignore=true install' 
            }
            post {
                success {
                    junit 'target/surefire-reports/**/*.xml' 
                }
            }  
        }
        
        stage ('Deploy'){
          steps{
            sh  'echo "deploying into qa server"'
            }
        }
    }
  
}
