pipeline {
  agent any 
  tools {
        //jdk 'jdk11'
        maven 'maven3'
                
    }
    environment {
        sonarUrl = 'sonar.host.url=http://172.17.0.3:9000'
	sonarToken = "sonar.login=${sonarToken}"
    }
   // This is to demo github action	
   //def sonarUrl = 'sonar.host.url=http://172.17.0.2:9000'
   //def mvnHome = tool name: 'maven3', type: 'maven'
   //def scannerHome = tool 'sonar_scanner'
 stages {
   /*stage('GitClone'){
	steps { 
	   deleteDir()
  	   checkout scm
           // Clone repo
	   sh 'git clone https://github.com/fmfjunior/ExampleJavaProject'   
	  }
    }*/
   
     stage('MvnPackage'){
	 // Build using maven
	   //Get Maven Home Path
	   steps { 
	     sh 'mvn clean package -DskipTest=true'
	   }  
    }
	 
	 
     stage( 'Teste Unitario') {
	 steps { 
	   //junit 'reports/**/*.xml'
	   junit allowEmptyResults: true, testResults: 'target/surefire-reports/*.xml'
	   sh 'mvn clean jacoco:prepare-agent install'
           //sh 'mvn jacoco:report'
	 }
    } 
	 
   
     stage( 'Scanner sonar') {
          /*environment {
                scannerHome = tool 'sonar_scanner'
          }*/
          steps{
        	//sh "${mvn} sonar:sonar -D${sonarUrl}  -D${sonarToken}"
                sh "mvn sonar:sonar-D${sonarUrl}  -D${sonarToken}"
		//withSonarQubeEnv('sonar_server'){
                //sh "${scannerHome}/bin/sonar-scanner -Dsonar.projectKey=devops -Dsonar.host.url=http://172.17.0.3:9000 -Dsonar.java.binaries=target -Dsonar.coverage.exclusions=**/mvm**,**/src/test/**,**/model/** -Dsonar.junit.reportPath=target/surefire-reports -Dsonar.jacoco.reportPath=target/jacoco.exec" 
                //}
          }
      }
 }

}
  
  
  /*stage('Code QA') {
	    withCredentials([string(credentialsId: 'SonarToken', variable: 'sonarToken')]) {
       	    def sonarToken = "sonar.login=${sonarToken}"
            sh "${mvnHome}/bin/mvn sonar:sonar -D${sonarUrl}  -D${sonarToken}"
	    }
   }*/

    //stage('Sonar Publish'){
	//withCredentials([string(credentialsId: 'SonarToken', variable: 'sonarToken')]) {
        //def sonarToken = "sonar.login=${sonarToken}"
        //sh "${mvn} sonar:sonar -D${sonarUrl}  -D${sonarToken}"
	 //}
      
   //}
   
  // stage('deploy-dev'){
    //   def tomcatDevIp = '172.31.28.172'
	   //def tomcatHome = '/opt/tomcat8/'
	   //def webApps = tomcatHome+'webapps/'
	   //def tomcatStart = "${tomcatHome}bin/startup.sh"
	   //def tomcatStop = "${tomcatHome}bin/shutdown.sh"
	   
	   //sshagent (credentials: ['tomcat-dev']) {
	     // sh "scp -o StrictHostKeyChecking=no target/myweb*.war ec2-user@${tomcatDevIp}:${webApps}myweb.war"
       //   sh "ssh ec2-user@${tomcatDevIp} ${tomcatStop}"
		 // sh "ssh ec2-user@${tomcatDevIp} ${tomcatStart}"
       //}
  // }
  // stage('Email Notification'){
	//	mail bcc: '', body: """Hi Team, You build successfully deployed
	//	                       Job URL : ${env.JOB_URL}
	//						   Job Name: ${env.JOB_NAME}
// Thanks,
// DevOps Team""", cc: '', from: '', replyTo: '', subject: "${env.JOB_NAME} Success", to: 'hari.kammana@gmail.com'
   

