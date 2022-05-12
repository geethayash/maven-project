node {
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
    
}
stage('email notification')
{
    mail bcc: '', body: 'Build success', cc: '', from: '', replyTo: '', subject: 'jenkins build info', to: 'ankishettygeetha45@gmail.com'
}
}
