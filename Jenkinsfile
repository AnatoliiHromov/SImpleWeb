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
            sh 'mvn clean install test package"'      
       
            
        }
    }
        
    }
}
           
