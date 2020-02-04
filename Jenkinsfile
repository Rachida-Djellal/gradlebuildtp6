pipeline {
  agent any
  stages {
    stage('Build') {
      steps {
        bat 'gradle build '
        bat 'gradle javadoc'
        archiveArtifacts 'build\\docs\\javadoc\\*'
        junit 'build\\test-results\\test\\*.xml'
      }
    }

    stage('Mail Notification') {
      steps {
        mail(to: 'gr_djellal@esi.dz', subject: 'tpoutil', body: 'vwgwbg', replyTo: 'gr_djellal@esi.dz')
      }
    }

    stage('code analysis') {
      parallel {
        stage('code analysis') {
          steps {
            withSonarQubeEnv('sonar') {
              bat 'C:\\Users\\Djallal\\Desktop\\2cs\\outil1\\gradle-6.0.1\\bin\\gradle sonarQube'
            }

            waitForQualityGate true
          }
        }

        stage('Test reporting') {
          steps {
            jacoco()
          }
        }

      }
    }

    stage('Deployment') {
      when {
        branch 'master'
      }
      steps {
        bat 'C:\\Users\\Djallal\\Desktop\\2cs\\outil1\\gradle-6.0.1\\bin\\gradle publish'
      }
    }

    stage('slack ') {
      when {
        branch 'master'
      }
      steps {
        slackSend(token: 'TRC4DGSAE/BT62RMTU2/xkDQOCImpl3xUisvsWjf0K0T', baseUrl: 'https://hooks.slack.com/services/', teamDomain: 'hooks', channel: '#matrix', message: 'terminer')
      }
    }

  }
}