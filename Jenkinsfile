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
      steps {
        bat 'C:\\Users\\Djallal\\Desktop\\2cs\\outil1\\gradle-6.0.1\\bin\\gradle publish'
      }
    }

  }
}