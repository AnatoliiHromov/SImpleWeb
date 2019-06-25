#!groovy
// Check ub1 properties
properties([disableConcurrentBuilds()])
properties([pipelineTriggers([githubPush()])])

pipeline {
        agent {
            label 'ubuntu'
        }   
 
        options {
        buildDiscarder(logRotator(numToKeepStr: '5', artifactNumToKeepStr: '5'))
        timestamps()
    }
           tools { 
            maven 'maven' 
        }
    stages {
     stage ('Checkout'){
         steps{
        git branch: 'master', url: 'https://github.com/AnatoliiHromov/SImpleWeb.git'
         }
     }
      stage ('Build'){
          steps{
              
             echo "!______________Build-----------------------"      
            sh 'mvn clean install test package'      
       
            
        }
    }
      stage ('Deploy'){
           steps {
                echo '!______________deploy -----------------------'
                sh "curl -u deploy:12345 --upload-file /home/jenkins/workspace/MavenWebPipeline/webapp/target/TryBuildAndDeploy.war "http://ec2-35-176-16-201.eu-west-2.compute.amazonaws.com:8080/manager/deploy?path=/debug&update=true""
            }
           }
        
    }
}
           
