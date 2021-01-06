pipeline {
  agent {
    node {
      label 'Linux'
    }

  }
  stages {
    stage('Clone') {
      steps {
        git(url: 'https://github.com/dwz99/devops-webapp2', branch: 'master', poll: true)
      }
    }

    stage('Build') {
      parallel {
        stage('Build') {
          steps {
            sh '''whoami
date
echo $PATH
pwd
ls -la
./gradlew build --info'''
          }
        }

        stage('P1') {
          steps {
            sh '''date
echo run parallel !!'''
          }
        }

        stage('P2') {
          steps {
            sh '''date
echo run parallel !!'''
          }
        }

      }
    }

    stage('Publish') {
      steps {
        archiveArtifacts(artifacts: 'build/libs/*.war', fingerprint: true, onlyIfSuccessful: true)
      }
    }

  }
}