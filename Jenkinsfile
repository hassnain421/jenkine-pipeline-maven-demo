node {
  stage ('Cloning from Git'){
    git 'https://github.com/hassnain421/jenkine-pipeline-maven-demo.git'
  }
  stage ('Execute Maven'){
    tool name: 'maven3.8.2', type: 'maven'
    sh 'mvn clean install'    
  }
}
