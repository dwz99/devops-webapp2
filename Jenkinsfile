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
            sh '''RELEASE=webapp.war
pwd
./gradlew build -Pwarname=$RELEASE --info
ls -la build/libs/
cp ./build/libs/$RELEASE ./docker'''
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

    stage('Packaging') {
      steps {
        sh '''pwd
cd ./docker
docker build -t docker.sas.com/webapp2-2020:$BUILD_ID .
docker tag docker.sas.com/webapp2-2020:$BUILD_ID docker.sas.com/webapp2-2020:latest
docker images'''
      }
    }

    stage('Publish') {
      steps {
        script {
          withCredentials([usernamePassword(credentialsId: 'sas-dockerhub', usernameVariable: 'DOCKER_USERNAME', passwordVariable: 'DOCKER_PASSWORD')]){
            sh '''
docker login docker.sas.com -u="$DOCKER_USERNAME" -p="$DOCKER_PASSWORD"
docker push docker.sas.com/webapp2-2020:$BUILD_ID
docker push docker.sas.com/webapp2-2020:latest
'''
          }
        }

      }
    }

  }
}