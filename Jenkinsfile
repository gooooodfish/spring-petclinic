node {
  stage('change java'){
    jdk = tool name: 'Java17'
    env.JAVA_HOME = "${jdk}"
    echo "jdk installation path is: ${jdk}"
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
  stage('BUILD'){
    def mvn = tool 'Default Maven';
    sh "${mvn}/bin/mvn package"
    sh "java -jar target/*.jar"
  }
}