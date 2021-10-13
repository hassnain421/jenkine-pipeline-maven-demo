node {
  stage ('Cloning from Git') {
    git 'https://github.com/hassnain421/jenkine-pipeline-maven-demo.git'
  }
  stage ('Execute Maven') {
    mvnHome = tool 'maven'
    sh 'mvn clean install'    
  }
  stage ('SonarQube Analysis') {
    def scannerHome = tool 'sonarqube';
    withSonarQubeEnv('sonarqube') {
      sh """${scannerHome}/bin/sonar-scanner \
      -Dsonar.login = admin \
      -Dsonar.password = 1234 \
      -DsonarBaseDir = var/lib/jenkins/workspace/maven/ \
      -Dsonar.projectKey = testmaven \
      -Dsonar.sources=. \
      -Dsonar.host.url=http://143.198.7.75:9000/"""
    }
  }
}
