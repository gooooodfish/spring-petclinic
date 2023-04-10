node {
  stage('Java Version Change'){
    jdk = tool name: 'Java17'
    env.JAVA_HOME = "${jdk}"
    env.PATH="${env.JAVA_HOME}/bin:${env.PATH}"
    echo "jdk installation path is: ${jdk}"
  }
  stage('SCM') {
    checkout scm
  }
  stage('SonarQube Analysis') {
    jdk = tool name: 'Java17'
    env.JAVA_HOME = "${jdk}"
    env.PATH="${env.JAVA_HOME}/bin:${env.PATH}"
    def mvn = tool 'Default Maven';
    withSonarQubeEnv() {
      sh "${mvn}/bin/mvn clean verify sonar:sonar -Dsonar.projectKey=petclinic"
    }
  }
  stage('BUILD'){
    def mvn = tool 'Default Maven';
    sh "${mvn}/bin/mvn package"
  }
}