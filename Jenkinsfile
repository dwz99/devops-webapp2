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
      steps {
        sh '''whoami
date
echo $PATH
pwd
ls -la
./gradlew build --info'''
      }
    }

    stage('Publish') {
      steps {
        archiveArtifacts(artifacts: 'build/lib/*.war', fingerprint: true, onlyIfSuccessful: true)
      }
    }

  }
}