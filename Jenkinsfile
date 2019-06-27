#!groovy
// Check ub1 properties
properties([disableConcurrentBuilds()])


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
                echo '!______________deploy y-----------------------'
                withCredentials([usernamePassword(credentialsId: 'tomcat', usernameVariable: 'USERNAME', passwordVariable: 'PASSWORD')]) {
                sh 'curl -v -u $USERNAME:$PASSWORD --upload-file /home/jenkins/workspace/MavenWebPipeline/webapp/target/TryBuildAndDeploy.war "http://35.177.144.95:8080/manager/text/deploy?path=/TryBuildAndDeployPipe.war&update=true"'
            }
           }
      }
    }
}
           
