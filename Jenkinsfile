#!groovy
// Check ub1 properties
properties([disableConcurrentBuilds()])


pipeline {
        agent {
            label 'ubuntu'
        }   
        triggers { pollSCM('* * * * *') }
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
                echo '!______________deploy y-----------------------'
                withCredentials([usernamePassword(credentialsId: 'tomcat', usernameVariable: 'USERNAME', passwordVariable: 'PASSWORD')]) {
                sh 'curl -v -u $USERNAME:$PASSWORD --upload-file /home/jenkins/workspace/MavenWebPipeline/webapp/target/TryBuildAndDeploy.war "http://ec2-35-176-16-201.eu-west-2.compute.amazonaws.com:8080/manager/text/deploy?path=/home/jenkins/workspace/MavenWebPipeline/webapp/target/TryBuildAndDeploy.war&update=true"'
            }
           }
      }
    }
}
           
