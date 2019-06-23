pipeline {
    agent any
    stages
    {
       
        stage('Git Clone')
        {
            steps{
            sh 'rm -rf spring3hibernate;  git clone https://github.com/Deveshs23/spring3hibernate.git'
            }
        }
        stage('Email Notification')
        {
            steps{
            mail bcc: '', body: 'Going to Start Deployment', cc: '', from: '', replyTo: '', subject: 'Opstree_Ninja', to: 'deveshs2221@gmail.com'                }
                
            }
        stage('Slack Notification')
        {
            steps{
            slackSend channel: 'ot-ninja-batch-5', color: 'green', iconEmoji: '', message: 'Going to start Deployment', tokenCredentialId: 'MEhmTzCjD8CHkUmva43pSUpM','Slack_Notification', username: ''
                }
                
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
                  cobertura autoUpdateHealth: false, autoUpdateStability: false, coberturaReportFile: '/target/site/cobertura/coverage.xml', conditionalCoverageTargets: '70, 0, 0', enableNewApi: true, failUnhealthy: false, failUnstable: false, lineCoverageTargets: '80, 0, 0', maxNumberOfBuilds: 0, methodCoverageTargets: '80, 0, 0', onlyStable: false, sourceEncoding: 'ASCII', zoomCoverageChart: false
                  checkstyle()
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
                sh 'cd spring3hibernate; cp /target/Spring3HibernateApp.war /var/lib/tomcat8/webapps/'
            }    
        }
        stage('Slack Final Notification')
        {
            steps{
                slackSend channel: 'ot-ninja-batch-5', color: 'green', iconEmoji: '', message: 'Hurray', tokenCredentialId: 'Slack_Notification', username: ''
                
            }
        }
        
         }

      }
        

