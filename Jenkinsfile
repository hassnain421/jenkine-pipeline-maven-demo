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
      sh "${scannerHome}/bin/sonar-scanner \
      -D sonar.login=admin \
      -D sonar.password=1234 \
      -D sonar.projectKey=test \
      -D sonar.sources=/var/lib/jenkins/workspace/testqualitygate/src/main/java/com/github/wololock/ \
      -D sonar.tests=/var/lib/jenkins/workspace/testqualitygate/src/test/java/com/github/wololock/ \
      -D sonar.host.url=http://192.168.2.3:30958/"
    }
  }
  stage("Quality Gate") {
        timeout(time: 1, unit: 'HOURS') {
            waitForQualityGate abortPipeline: true
        }
  }
  
}
