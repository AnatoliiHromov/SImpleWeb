#!groovy
// Check ub1 properties
properties([disableConcurrentBuilds()])
properties([pipelineTriggers([githubPush()])])

pipeline {
        agent {
            label 'ubuntu'
        }   
        tools { 
            maven 'maven' 
        }
        options {
        buildDiscarder(logRotator(numToKeepStr: '5', artifactNumToKeepStr: '5'))
        timestamps()
    }
    stages {
     stage ('Checkout'){
        git branch: 'master', url: 'https://github.com/AnatoliiHromov/SImpleWeb.git'
    }
      stage ('Build'){
          steps{
             echo {
                 message '!______________Build-----------------------'
            }
              dir ('MavenPipe') {
                  sh "${mvnHome}/home/jenkins/tools/hudson.tasks.Maven_MavenInstallation/maven/bin/mvn clean install test package"
            }
        }
    }
        
    }
}
           
