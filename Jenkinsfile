pipeline{
  agent any
  tools{
    jdk 'Java17'
  }
  stages{
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
        withSonarQubeEnv('sonarqube') {
          sh "${mvn}/bin/mvn clean verify sonar:sonar -Dsonar.projectKey=petclinic"
        }
      }
    }
  }
}