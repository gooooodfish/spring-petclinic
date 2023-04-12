node {
  stage('Java Version Change'){
    jdk = tool name: 'JDK-17'
    env.JAVA_HOME = "${jdk}"
    env.PATH="${env.JAVA_HOME}/bin:${env.PATH}"
    echo "jdk installation path is: ${jdk}"
  }
  stage('SCM') {
    checkout scm
  }
  stage('SonarQube Analysis') {
    def mvn = tool 'Default Maven';
    withSonarQubeEnv() {
      sh "${mvn}/bin/mvn clean verify sonar:sonar -Dsonar.projectKey=petclinic1 -Dsonar.projectName='petclinic1'"
    }
  }
  stage('BUILD'){
    def mvn = tool 'Default Maven';
    sh "${mvn}/bin/mvn package"
  }
}