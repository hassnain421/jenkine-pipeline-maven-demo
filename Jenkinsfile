node {
  stage ('Cloning from Git') {
    git 'https://github.com/hassnain421/jenkine-pipeline-maven-demo.git'
  }
  stage ('Execute Maven') {
    tool name: 'maven3.8.2', type: 'mav'
    sh 'mvn clean install'    
  }
  stage ('SonarQube Analysis') {
    def scannerHome = tool 'sonarqube';
    withSonarQubeEnv('sonarqube') {
      sh """$(scannerHome)/sonarqube/bin/sonar-scanner \
      -D sonar.login = admin \
      -D sonar.password = 1234 \
      -D sonarBaseDir = var/lib/jenkins/workspace/maven/ \
      -D sonar.projectKey = maven \
      -D sonar.tests= /var/lib/jenkins/workspace/maven/src/main
      -D sonar.tests= /var/lib/jenkins/workspace/maven/src/test
      -D sonar.host.url=http://143.198.7.75:9000/"""
    }
  }
}
