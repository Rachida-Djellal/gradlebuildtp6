pipeline {
  agent any
  stages {
    stage('build') {
      steps {
        bat 'gradle build'
        bat 'gradle javadoc'
        archiveArtifacts 'build/libs/**/*.jar'
        archiveArtifacts 'build/docs/javadoc/**'
        junit 'build/test-results/test/*.xml'
      }
    }

    stage('Mail Notification') {
      steps {
        mail(subject: 'Test Jenkins', body: 'heloo', to: 'gr_djellal@esi.dz',  replyTo: 'gr_djellal@esi.dz')
      }
    }



        stage('Test Reporting') {
          steps {
            jacoco(classPattern: 'src/main/java/com.example/**/*.java', exclusionPattern: 'src/test/java/com.test/*.java', sourcePattern: 'src/**')
          }
        }


    stage('Deployement') {
      when{
        expression{
          env.CHANGE_ID == NULL
        }
      }

      steps {
        bat 'gradle publish'
      }
    }

    stage('Slack Notification') {
      when{
        expression{
           env.CHANGE_ID == NULL
        }
      }
      steps {
        slackSend(channel: '#matrix', message: 'heyoooo jenkins', sendAsText: true, notifyCommitters: true, replyBroadcast: true, token: 'TRC4DGSAE/BT9KX62SD/8hNqTU307xAQSKpvJFlk5ID3', baseUrl: 'https://hooks.slack.com/services', teamDomain: 'hooks')
      }
    }

  }
}
