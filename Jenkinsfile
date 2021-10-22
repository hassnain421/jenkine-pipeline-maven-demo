node {
  stage ('Cloning from Git') {
    git 'https://github.com/hassnain421/jenkine-pipeline-maven-demo.git'
  }
  stage ('Execute Maven') {
    mvnHome = tool 'maven'
    sh 'mvn clean install'    
  }
/*
  stage('SonarQube Analysis') {
    def mvn = tool 'maven';
    withSonarQubeEnv() {
      sh "${mvn}/bin/mvn clean verify sonar:sonar"
    }
  }*/
 stage ('SonarQube Analysis') {
    def scannerHome = tool 'sonarqube';
    withSonarQubeEnv('sonarqube') {
      sh """${scannerHome}/bin/sonar-scanner \
      -D sonar.login = admin \
      -D sonar.password = 1234 \
      -D sonar.projectKey = maven \
      -D sonar.projectBaseDir=/var/lib/jenkins/workspace/maven/ \
      -D sonar.sources= maven/src/main/ \
      -D sonar.tests= maven/src/test/ \
      -D sonar.host.url=http://192.168.161.130:9000/"""
    }
  }
  
}
