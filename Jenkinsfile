node {
  stage('Peek Java'){
      sh '''
        env | grep -e PATH -e JAVA_HOME
        which java
        java -version
      '''
  }
  stage('SCM') {
    checkout scm
  }
  stage('SonarQube Analysis') {
    def mvn = tool 'Default Maven';
    withSonarQubeEnv() {
      sh "${mvn}/bin/mvn clean verify sonar:sonar -Dsonar.projectKey=petclinic"
    }
  }
}