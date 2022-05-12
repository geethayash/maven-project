node {
    parameters {
  string defaultValue: 'dev', name: 'ENV'
  // choice choices: ['L1', 'L2', 'L3'], name: 'Level'
  }
    stage('git checkout') {
    checkout([$class: 'GitSCM', branches: [[name: '*/master']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/AnupamaSoma/maven-project.git']]])
    }
 stage('maven build') {
    sh 'mvn package'
}
stage('QA deployment')
{
    deploy adapters: [tomcat9(credentialsId: 'tomcat-credentials2', path: '', url: 'http://172.31.9.230:8080')], contextPath: 'test', war: '**\\*.war'
}
stage('testing')
{
    git 'https://github.com/AnupamaSoma/FunctionalTesting.git'
    sh 'java -jar /var/lib/jenkins/workspace/scripted/testing.jar'
}
stage('prod deployment')
{
 deploy adapters: [tomcat9(credentialsId: 'tomcat-credentials2', path: '', url: 'http://172.31.10.102:8080')], contextPath: 'prod', war: '**\\*.war'
  echo "${params.ENV}"  

    
    
}
}
