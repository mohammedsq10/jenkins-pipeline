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
        echo "++++++++++Java Run++++++++++++++"
        java -jar /var/lib/jenkins/workspace/maven/target/*.jar
        echo '>>> End building using Maven'
      }
    }
  }
}
