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
                 git branch: 'dev', credentialsId: '17cbc593-ebf6-481d-8538-ceeee47a499e', url: 'https://github.com/M-sDevOpsCareer/Facebook.git'
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
                sh 'mvn clean sonar:sonar'//credentials in pom.xml file 
             }
        }
        stage('UploadArtifactsIntoNexusServer') 
         {
             steps 
             {
                sh 'mvn clean deploy'//nexus repo urls in pom.xml & credentials in jenkins/tools/maven dir settings.xml file 
             }
        }
    }
}
