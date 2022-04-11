node {
    stage('Continous Download') {
    checkout([$class: 'GitSCM', branches: [[name: '*/master']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/AnupamaSoma/maven-project.git']]])
}
stage('Continous Build') {
    sh 'mvn package'
}
stage('Continous Deployment'){
    deploy adapters: [tomcat9(credentialsId: 'tomcat-credentials', path: '', url: 'http://172.31.31.62:8080')], contextPath: 'qaapp', war: '**\\*.war'
}
stage('Continous Testing')
{
    git 'https://github.com/AnupamaSoma/FunctionalTesting.git'
    sh 'java -jar /var/lib/jenkins/workspace/scripted_pipeline/testing.jar'
}
stage('Continous DElivery'){
    deploy adapters: [tomcat9(credentialsId: 'tomcat-credentials', path: '', url: 'http://172.31.17.232:8080')], contextPath: 'prodapp', war: '**\\*.war'
}
stage('Email Notifiacation')
{
   mail bcc: '', body: 'It is successfull', cc: '', from: '', replyTo: '', subject: 'Jenkins build', to: 'priyanjali.soma@gmail.com'
}

}
