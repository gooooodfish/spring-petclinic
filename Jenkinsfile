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
      sh "${mvn}/bin/mvn clean verify sonar:sonar -Dsonar.login=${env.SONAR_ID} -Dsonar.password=${env.SONAR_PASSWORD} -Dsonar.projectKey=petclinic -Dsonar.projectName='petclinic'"
    }
  }
  stage('BUILD'){
    def mvn = tool 'Default Maven';
    sh "${mvn}/bin/mvn package"
  }
}