 pipeline {
  tools {
    maven 'Maven3.8.3'
  }
    agent any
    stages {
     stage('Slack message'){
      steps{
       slackSend color :'#BADA55' , message :'Successfull!!'
      }
     }
        stage('Clean') {
            steps {
                echo 'Cleaning..'
                bat 'mvn -B -DskipTests clean'
            }
        }
      post {
        always {
            emailext body: 'A Test EMail', recipientProviders: [[$class: 'DevelopersRecipientProvider'], [$class: 'RequesterRecipientProvider']], subject: 'Test'
        }
    }
      
        stage('Test') {
            steps {
                echo 'Testing..'
                bat 'mvn test'
            }
             post {
                always {
                    junit 'target/surefire-reports/*.xml'
                }
            }
        }
        stage('Package') {
            steps {
                echo 'mvn package'
            }
        }
     
    }
}
 
