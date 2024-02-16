pipeline {

    agent any
    
    tools{
      maven "MAVEN3"
      jdk "OracleJDK8"
    }
      
        environment {
        NEXUS_USER = 'admin'
        NEXUS_PASS = 'Gabbar$8'
        NEXUSIP = '172.200.227.229'
        NEXUSPORT = '8081'
        RELEASE_REPO ='vprofile-release'
        NEXUS_GRP_REPO ='vpro-maven-group'
        NEXUS_CREDENTIAL_ID = 'nexuslogin'
        CENTRAL_REPO = 'vpro-maven-central'

        SONARSERVER = 'sonarserver'
        SONARSCANNER ='sonarscanner'

    //     NEXUS_VERSION = "nexus3"
    //     NEXUS_PROTOCOL = "http"
    //     http://172.200.227.229:8081/
    //    NEXUS_URL = "172.200.227.229:8081"
    //     NEXUS_REPOSITORY = "vprofile-release"
	  //     NEXUS_REPOGRP_ID= "vprofile-grp-repo"
    //     NEXUS_CREDENTIAL_ID = "nexuslogin"
    //     ARTVERSION = "${env.BUILD_ID}"
    }
   stages{
      stage('BUILD'){
        steps {
            sh 'mvn -s settings.xml -DskipTests install'
         }
         post{
          success {
            echo "Now Archiving"
            archiveArtifacts artifacts: '**/*.war'
          }
         }
      }
        stage('TEST'){
        steps {
            sh 'mvn test'
         }
       }
        stage('CheckStyle Analysis'){
        steps {
            sh 'mvn checkstyle:checkstyle'
         }

        }
        stage('CODE ANALYSIS with SONARQUBE') {
          
		  environment {
             scannerHome = tool "${sonarscanner}"
          }

          steps {
            withSonarQubeEnv("${SONARSERVER}") {
               sh '''${scannerHome}/bin/sonar-scanner -Dsonar.projectKey=vprofile \
                   -Dsonar.projectName=vprofile-repo \
                   -Dsonar.projectVersion=1.0 \
                   -Dsonar.sources=src/ \
                   -Dsonar.java.binaries=target/test-classes/com/visualpathit/account/controllerTest/ \
                   -Dsonar.junit.reportsPath=target/surefire-reports/ \
                   -Dsonar.jacoco.reportsPath=target/jacoco.exec \
                   -Dsonar.java.checkstyle.reportPaths=target/checkstyle-result.xml'''

               }    
          } 
            
      
    }
  }
}