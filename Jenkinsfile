pipeline{
  agent any
  tools{
    jdk 'Java17'
  }
  stage('Peek Java'){
    steps{
      sh '''
        env | grep -e PATH -e JAVA_HOME
        which java
        java -version
      '''
    }
  }

  stage('Peek Java'){
    steps{
      sh '''
        env | grep -e PATH -e JAVA_HOME
        which java
        java -version
      '''
    }

  }
  stage('SCM') {
    steps{
      checkout scm
    }
  }
  stage('SonarQube Analysis') {
    environment{
      mvn = tool 'Default Maven';
    }

    steps{
      withSonarQubeEnv() {
        sh "${mvn}/bin/mvn clean verify sonar:sonar -Dsonar.projectKey=petclinic"
      }
    }
  }
}