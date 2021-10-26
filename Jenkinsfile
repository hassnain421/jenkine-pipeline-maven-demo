nnode {
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
      sh "${scannerHome}/bin/sonar-scanner \
      -D sonar.projectVersion=1.0-SNAPSHOT \      
      -D sonar.login=admin \
      -D sonar.password=12345 \
      -D sonar.projectKey=maven2 \
      -D sonar.sources=/var/lib/jenkins/workspace/maven/src/main/ \
      -D sonar.tests=/var/lib/jenkins/workspace/maven/src/test/ \
      -D sonar.host.url=http://192.168.161.133:9000/"
    }
  }
  
}
