node('built-in')
{
    stage('ContinuousDownload') 
    {
       git 'https://github.com/intelliqittrainings/maven.git'
    }
    stage('ContinuousBuild') 
    {
       sh 'mvn package'
    }
    stage('ContinuousDeployment') 
    {
       deploy adapters: [tomcat9(credentialsId: 'fbb086d7-3de2-4add-9a78-176dd968cc16', path: '', url: 'http://172.31.21.45:8080')], contextPath: 'testapp', war: '**/*.war'
    } 
    stage('ContinuousTesting') 
    {
       git 'https://github.com/intelliqittrainings/FunctionalTesting.git'
       sh  'java -jar /var/lib/jenkins/workspace/ScriptedPipeline2/testing.jar'
    }
     stage('ContinuousDelivery') 
    {
          input message: 'Need approval from king', submitter: 'viratkohli'
           deploy adapters: [tomcat9(credentialsId: 'fbb086d7-3de2-4add-9a78-176dd968cc16', path: '', url: 'http://172.31.25.60:8080')], contextPath: 'prodapp', war: '**/*.war'
    }
    
}

