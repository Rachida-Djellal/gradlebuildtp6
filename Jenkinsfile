pipeline {
  agent any
  stages {
    stage('Build') {
      steps {
        bat 'gradle build '
        bat 'gradle javadoc'
        archiveArtifacts 'build\\docs\\javadoc\\*'
        junit 'build\\test-results\\test\\.xml'
      }
    }

  }
}