pipeline {
  agent any
  stages {
    stage('SCM Checkout') {
      steps {
        echo '>>> Start getting SCM code'
        git 'https://github.com/mohammedsq10/demo1.git'
        echo '>>> End getting SCM code'
      }
    }

    stage('Build JAR') {
      steps {
        echo '>>> Start building using Maven'
        sh 'mvn -Dmaven.test.skip=TRUE install'
        echo '>>> End building using Maven'
      }
    }

    stage('Build Docker Image') {
      steps {
        echo '>>> start clearing old docker images'
        sh label: '', script: '''if docker images -a | grep "pipeline-demo*" | awk \'{print $1":"$2}\' | xargs docker rmi -f; then
         printf \'Clearing old images succeeded\\n\'
        else
          printf \'Clearing old images failed\\n\'
        fi'''
        echo '>>> End clearing old docker images'
        echo '>>> Start building App docker image'
        sh "docker build -t $MyDockerAccountName/$MyDockerReposioryName:$MyTagName$BUILD_NUMBER --pull=true $WORKSPACE"
        echo '>>> End building App docker image'
      }
    }
  }
}
