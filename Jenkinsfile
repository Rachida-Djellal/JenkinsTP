pipeline {
  agent any
  stages {
    stage('Build') {
      steps {
        bat 'gradle build'
        bat 'gradle javadoc'
        archiveArtifacts 'build/libs/**/*.jar'
      }
    }

    stage('Mail notification') {
      steps {
        mail(subject: 'test jenkins', body: 'hello', to: 'gr_djellal@esi.dz', replyTo: 'gr_djellal@esi.dz')
      }
    }

  }
}