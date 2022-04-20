pipeline
{
    agent any
    stages
     {
         stage('continuousDownloads') 
         {
             steps
             {
                 git 'https://github.com/intelliqittrainings/maven.git'
             }
         }
         stage('continuousBuild') 
         {
             steps
             {
                 sh 'mvn package'
             }
         }
         stage('continuousDeployment') 
         {
             steps
             {
                 deploy adapters: [tomcat9(credentialsId: 'e8720653-0361-4e59-9940-2568564e4488', path: '', url: 'http://172.31.17.35:8080')], contextPath: 'qaaap', war: '**/*.war'
             }
         }
         stage('Continuoustesting') 
         {
             steps
             {
                 git 'https://github.com/intelliqittrainings/FunctionalTesting.git'
             }
         }
     }
     post
     {
         success
         {
             input message: 'waiting for Approval', submitter: 'jhum'
             deploy adapters: [tomcat9(credentialsId: 'e8720653-0361-4e59-9940-2568564e4488', path: '', url: 'http://172.31.25.54:8080')], contextPath: 'prodaap', war: '**/*.war'
         }
         failure
         {
             mail bcc: '', body: '', cc: '', from: '', replyTo: '', subject: 'Jenkins CI-CD failed', to: 'maaharttasuni@gmail.com'
         }
     }
}
