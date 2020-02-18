pipeline {
  agent any
  stages {
    stage('Build') {
      steps {
        bat 'gradle build'
        bat 'gradle javadoc'
      }
    }

    stage('Mail notification') {
      steps {
        mail(subject: 'test enkins', body: 'hello', to: 'gr_djellal@esi.dz', replyTo: 'gr_djellal@esi.dz')
      }
    }

  }
}