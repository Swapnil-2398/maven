pipeline
{
    agent any
    stages
    {
        stage('ContDownload')
        {
            steps
            {
               git 'https://github.com/intelliqittrainings/maven.git' 
            }
        }
         stage('ContBuild')
        {
            steps
            {
               sh 'mvn package'
            }
        }
        stage('ContDeployment')
        {
            steps
            {
               deploy adapters: [tomcat9(credentialsId: 'fb143dd7-dabe-4fd5-b0b9-ca745533a65d', path: '', url: 'http://172.31.8.143:8080')], contextPath: 'test1', war: '**/*.war'
            }
        }
        stage('ContTesting')
        {
            steps
            {
               git 'https://github.com/intelliqittrainings/FunctionalTesting.git'
               sh 'java -jar /var/lib/jenkins/workspace/DeclarativePipeline1/testing.jar'
            }
        }
         stage('ContDelivery')
        {
            steps
            {
               deploy adapters: [tomcat9(credentialsId: 'fb143dd7-dabe-4fd5-b0b9-ca745533a65d', path: '', url: 'http://172.31.11.166:8080')], contextPath: 'prod1', war: '**/*.war'
            }
        }
    }
}
