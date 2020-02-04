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
        mail(to: 'gn_ahmime@esi.dz', subject: 'tpoutil', body: 'vwgwbg', from: 'gr_djellal@esi.dz')
      }
    }

    stage('code analysis') {
      steps {
        withSonarQubeEnv('sonar') {
          bat 'C:\\Users\\Djallal\\Desktop\\2cs\\outil1\\gradle-6.0.1\\bin\\gradle sonarQube'
        }

      }
    }

  }
}