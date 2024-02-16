pipeline{

    agent any
    
    tools{
      maven "MAVEN3"
      jdk "OracleJDK8"
    }
      
        environment {
        NEXUS_USER = "admin"
        NEXUS_PASS ="Gabbar$8"
        NEXUSIP ='10.0.0.4'
        NEXUSPORT = '8081'
        RELEASE_REPO =
        CENTRAL_REPO =
        NEXUS_GRP_REPO =

        NEXUS_VERSION = "nexus3"
        NEXUS_PROTOCOL = "http"
       NEXUS_URL = "172.200.227.229:8081"
        NEXUS_REPOSITORY = "vprofile-release"
	    NEXUS_REPOGRP_ID= "vprofile-grp-repo"
        NEXUS_CREDENTIAL_ID = "nexuslogin"
        ARTVERSION = "${env.BUILD_ID}"
    }
   stages{
      stage('BUILD'){
        steps {
            sh 'mav -s setting.xml -DskipTests install'
         }
      }


   }
}
