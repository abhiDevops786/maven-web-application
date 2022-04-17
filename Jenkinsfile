node {
    def mavenHome = tool name: "maven3.8.5"
    
    properties([buildDiscarder(logRotator(artifactDaysToKeepStr: '', artifactNumToKeepStr: '', daysToKeepStr: '', numToKeepStr: '5')), [$class: 'JobLocalConfiguration', changeReasonComment: ''], pipelineTriggers([pollSCM('* * * * *')])])
    
    stage("scm"){
        git branch: 'development', credentialsId: '05237800-c7ca-4554-a185-a2ecb0bfccb8', url: ' https://github.com/abhiDevops786/maven-web-application.git'
    }
    stage("build"){
        sh "${mavenHome}/bin/mvn clean package"
    }
    stage("sonarBuild"){
        sh "${mavenHome}/bin/mvn sonar:sonar"
    }
    stage("Artifact"){
        sh "${mavenHome}/bin/mvn deploy"
    }
    stage("deploy"){
        sshagent(['bf892940-edac-49a2-a15e-3dce0e4118c9']) {
          sh "scp -o StrictHostKeyChecking=no target/maven-web-application.war ec2-user@13.232.189.249:/opt/tomcat9/webapps/"
        }
        
    }
        
}
