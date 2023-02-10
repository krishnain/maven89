pipeline
{
    agent any
    stages
    {
        stage('ContDownload')
        {
            steps
            {
               git 'https://github.com/krishnain/maven89.git' 
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
                deploy adapters: [tomcat9(credentialsId: '30c1f4c1-c962-4596-b63a-b10cdf79e09d', path: '', url: 'http://172.31.57.12:9090')], contextPath: 'testapp', war: '**/*.war'
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
                input message: 'Need approval from DM!', submitter: 'srinivas'
                deploy adapters: [tomcat9(credentialsId: '30c1f4c1-c962-4596-b63a-b10cdf79e09d', path: '', url: 'http://172.31.59.208:9090')], contextPath: 'prodapp', war: '**/*.war'
            }
        }
        
        
        
        
        
        
    }
}
