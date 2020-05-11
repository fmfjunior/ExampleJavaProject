node {
   // This is to demo github action	
   def sonarUrl = 'sonar.host.url=http://172.17.0.2:9000'
  // def mvnHome = tool name: 'maven', type: 'maven'
  
    stages {
       stage('GitClone'){
	deleteDir()
  	checkout scm
    // Clone repo
	//git branch: 'master', 
	//credentialsId: 'github', 
	sh 'git clone https://github.com/fmfjunior/ExampleJavaProject'
	//url: 'https://github.com/fmfjunior/com.sonar.maven'
    }
      stage ( 'construindo' ) {
          steps {
              sh 'mvn clean package -DskipTest=true'
              }
          }
      stage( 'teste unitario') {
          steps{
              sh 'mvn test' 
              }
          }
      stage( 'teste estatio scanner sonar') {
                environment {
                    scannerHome = tool 'sonar_scanner'
                }
                steps{
                    withSonarQubeEnv('sonar_server'){
                    sh "${scannerHome}/bin/sonar-scanner -Dsonar.projectKey=devops -Dsonar.host.url=http://172.17.0.2:9000 -Dsonar.java.binaries=target -Dsonar.coverage.exclusions=**/mvm**,**/src/test/**,**/model/**" 
                    }
             }
        }
    }
    post {
        always {
            junit allowEmptyResults: true, testResults: 'target/surefire-reports/*.xml, api-test/target/surefire-reports/*.xml, functional-test/target/surefire-reports/*.xml, functional-test/target/failsafe-reports/*.xml'
            archiveArtifacts artifacts: 'target/tasks-backend.war, frontend/target/tasks.war', onlyIfSuccessful: true
        }
    }
}

/*node {

   // This is to demo github action	
   def sonarUrl = 'sonar.host.url=http://172.17.0.2:9000'
   def mvnHome = tool name: 'Maven', type: 'maven'
   stage('GitClone'){
	deleteDir()
  	checkout scm
    // Clone repo
	//git branch: 'master', 
	//credentialsId: 'github', 
	sh 'git clone https://github.com/fmfjunior/ExampleJavaProject'
	//url: 'https://github.com/fmfjunior/com.sonar.maven'
   
   }
   
   stage('MvnPackage'){
	 // Build using maven
	   //Get Maven Home Path
	  
	   sh "${mvnHome}/bin/mvn package"
	   sh "${mvnHome}/bin/mvn jacoco:prepare-agent"
	   sh "${mvnHome}/bin/mvn jacoco:report"
   }
   
	
	stage ('Sonar Analysis') { 
	environment {scannerHome = tool 'SONAR_SCANNER' } 
	steps { withSonarQubeEnv('SONAR_LOCAL') { 
	bat "${scannerHome}/bin/sonar-scanner -e -Dsonar.projectKey=DeployBack -Dsonar.host.url=http:/172.17.0.2/:9000 -Dsonar.login=2603757615bc4c8495f9c66d00fbf9c28e47bfb1 -Dsonar.java.binaries=target -Dsonar.coverage.exclusions=**/.mvn/**,**/src/test/**,**/model/**,**Application.java" 
	} 
	      } 
} 
	stage ('Quality Gate') { 
		steps { 
			sleep(5) timeout(time: 1, unit: 'MINUTES') { waitForQualityGate abortPipeline: true } 
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
   
   //}
