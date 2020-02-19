pipeline {
  agent any
  stages {
    stage('Build') {
      steps {
        bat 'gradle build'
        bat 'gradle javadoc'
        archiveArtifacts 'build/libs/**/*.jar'
        archiveArtifacts 'build/docs/javadoc/**'
        junit 'build/test-results/test/*.xml'
      }
    }

    stage('Mail notification') {
      steps {
        mail(subject: 'test jenkins', body: 'hello', to: 'gr_djellal@esi.dz', replyTo: 'gr_djellal@esi.dz')
      }
    }

    stage('Code Analysis') {
      parallel {
        stage('Code Analysis') {
          steps {
            withSonarQubeEnv('sonar') {
              bat 'gradle sonarQube'
            }

          }
        }

        stage('Test reporting') {
          steps {
            jacoco(classPattern: 'src/main/java/com/**/*.java', exclusionPattern: 'src/test/java/com/test/*.java', sourcePattern: 'src/**')
          }
        }

      }
    }

    stage('Deployement') {
      steps {
        bat 'gradle publish'
      }
    }

    stage('Slack Notification') {
      steps {
        slackSend(channel: '#matrix', message: 'heyoooo jenkins', notifyCommitters: true, replyBroadcast: true, sendAsText: true, baseUrl: 'https://hooks.slack.com/services', token: 'TRC4DGSAE/BT62RMTU2/xkDQOCImpl3xUisvsWjf0K0T', teamDomain: 'hooks')
      }
    }

  }
}