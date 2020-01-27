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
        mail(to: 'gr_djellal@esi.dz', subject: 'tpoutil', body: 'vwgwbg', bcc: 'bgfwb', cc: 'gbwg', charset: 'wb', from: 'rachida')
      }
    }

  }
}