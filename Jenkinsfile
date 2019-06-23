pipeline {
    agent any
    stages {
        stage('Git Clone')
        {
            steps{
            sh 'rm -rf spring3hibernate;  git clone https://github.com/Deveshs23/spring3hibernate.git'
            }
        }
       stage('Email Notification')
        {
            steps{
            mail bcc: '', body: 'Devesh going to deploy', cc: '', from: 'deveshs2221@gmail.com', replyTo: '', subject: 'test', to: 'deveshs23@gmail.com'
           }
       }
        stage('Slack Notification')
        {
            steps{
            slackSend color: 'green', iconEmoji: '', message: 'Devesh Going To Start Deployment', teamDomain: 'opstree', tokenCredentialId: 'Slack_Notification', username: ''                }
                
            }
        stage('Input Process')
        {
            steps{
            input 'Can We '
            }
        }
        stage('Code Stability')
        {
            steps{
            sh 'cd spring3hibernate; mvn compile'
            }
        }
        stage('Code quality')
       {
          steps{
          input 'Enter Your Input: '
          sh 'cd spring3hibernate; mvn checkstyle:checkstyle'
        //  checkstyle()
            }
      }
       stage('Code Coverage')
      {
           steps{
               sh 'cd spring3hibernate; mvn cobertura:cobertura'
          //     cobertura()
           }
       }
       stage('Publish coverage')
         {
           steps{
               sh 'cd spring3hibernate'
               findbugs canComputeNew: false, defaultEncoding: '', excludePattern: '', healthy: '', includePattern: '', pattern: '', unHealthy: ''
               checkstyle canComputeNew: false, defaultEncoding: '', healthy: '', pattern: '', unHealthy: '80'
               publishCoverage adapters: [coberturaAdapter('target/site/cobertura/coverage.xml')], sourceFileResolver: sourceFiles('NEVER_STORE')
                //  cobertura()
                }
         }        
        stage('Input Process / Abourt')
        {
            steps{
                input "Can do deployment ?"
            }
        }
        stage('War File Generate')
        {
            steps{
                sh 'cd spring3hibernate; mvn install'
            }
        }
        stage('deploy war file in tomcat')
        {
            steps{
                sh 'cd spring3hibernate; cd target; cp Spring3HibernateApp.war /var/lib/tomcat8/webapps/'
            }    
        }
        stage('Slack Final Notification')
        {
            steps{
                
                slackSend color: 'green', iconEmoji: '', message: 'Hurry', teamDomain: 'opstree', tokenCredentialId: 'Slack_Notification', username: ''                
            }
        }
        
         }

      }

post {
   success {
     slackSend color: 'green', iconEmoji: '', message: 'Deployment Successful', teamDomain: 'opstree', tokenCredentialId: 'Slack_Notification', username: ''                
            }

failure {
    slackSend color: 'green', iconEmoji: '', message: 'Deployment fail', teamDomain: 'opstree', tokenCredentialId: 'Slack_Notification', username: ''                
            
}
}

