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
                deploy adapters: [tomcat9(credentialsId: '8fecf384-aae9-4fed-9ca8-b03157e7bad4', path: '', url: 'http://172.31.89.191:8080')], contextPath: 'mytestapp', war: '**/*.war'
            }
        }
        stage('ContTesting')
        {
            steps
            {
                git 'https://github.com/intelliqittrainings/FunctionalTesting.git'
                sh 'java -jar /home/ubuntu/.jenkins/workspace/DeclarativePipeline1/testing.jar'
            }
        }
        stage('ContDelivery')
        {
            steps
            {
                /*input message: 'Require Approvals', submitter: 'srinivas'*/
                deploy adapters: [tomcat9(credentialsId: '8fecf384-aae9-4fed-9ca8-b03157e7bad4', path: '', url: 'http://172.31.89.73:8080')], contextPath: 'myprodapp', war: '**/*.war'
            }
        }
    }
}
