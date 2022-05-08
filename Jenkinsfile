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
    deploy adapters: [tomcat9(credentialsId: 'tomcat-credentials', path: '', url: 'http://172.31.25.242:8080')], contextPath: 'test', war: '**\\*.war'
}
stage('testing')
{
    git 'https://github.com/AnupamaSoma/FunctionalTesting.git'
    sh 'java -jar /var/lib/jenkins/workspace/scripted/testing.jar'
}
stage('prod deployment')
{
        deploy adapters: [tomcat9(credentialsId: 'tomcat-credentials', path: '', url: 'http://172.31.26.23:8080')], contextPath: 'prod', war: '**\\*.war'

}
stage('email notification')
{
    mail bcc: '', body: 'Build is success', cc: '', from: '', replyTo: '', subject: 'Jenkins build Info', to: 'priyanjali.soma@gmail.com'
echo "${params.ENV}"
    
}
}
