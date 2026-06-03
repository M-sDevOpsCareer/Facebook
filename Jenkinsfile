pipeline 
{
    agent any
    tools
    {
    maven 'maven3.9.11'    
    }
      stages {
         stage('CheckoutCode') 
         {
             steps 
             {
                 git branch: 'master', credentialsId: '17cbc593-ebf6-481d-8538-ceeee47a499e', url: 'https://github.com/M-sDevOpsCareer/Facebook.git'
            }
        }
        stage('build') 
         {
             steps 
             {
                sh 'mvn clean package' 
             }
        }
      stage('SonarReport') 
         {
             steps 
             {
                withSonarQubeEnv('SonarQubeIntegrationWithJenkins') 
                {
                sh 'mvn clean sonar:sonar'//credentials in pom.xml file 
                }
             }    
        }
        stage('UploadArtifactsIntoNexusServer') 
         {
             steps 
             {
                nexusArtifactUploader artifacts: [[artifactId: 'maven-standalone-application', classifier: '', file: '/var/lib/jenkins/workspace/declarative-project/target/maven-standalone-application-0.0.1-SNAPSHOT.jar', type: 'jar']], credentialsId: 'Jenkinsnexus', groupId: 'com.mt', nexusUrl: '192.168.10.128:8081/repository/facebook-snapshot/', nexusVersion: 'nexus2', protocol: 'http', repository: 'facebook-snapshot', version: '0.0.1-SNAPSHOT'
                //mvn clean deploy command doesn't required because we are not push artifacts with te help of maven jenkins we take care.
             }
        } 
    }
}
