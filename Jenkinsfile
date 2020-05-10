node {

   // This is to demo github action	
   def sonarUrl = 'sonar.host.url=http://172.17.0.2:9000'
   def mvnHome = tool name: 'Maven', type: 'maven'
   stage('SCM Checkout'){
	deleteDir()
  	checkout scm
    // Clone repo
	//git branch: 'master', 
	//credentialsId: 'github', 
	sh 'git clone https://github.com/fmfjunior/com.sonar.maven'
	//url: 'https://github.com/fmfjunior/com.sonar.maven'
   
   }
   
   stage('Mvn Package'){
	 // Build using maven
	   //Get Maven Home Path
	  
	   sh "${mvnHome}/bin/mvn package"
   }
   
   stage('Sonarqube') {
	    withCredentials([string(credentialsId: 'SonarToken', variable: 'sonarToken')]) {
       	    def sonarToken = "sonar.login=${sonarToken}"
            sh "${mvnHome}/bin/mvn sonar:sonar -D${sonarUrl}  -D${sonarToken}"
	    }
   }

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
   
   //}
}
