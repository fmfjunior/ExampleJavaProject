pipeline {
  agent any 
  tools {
        jdk 'jdk11'
        maven 'maven3'
                
    }
    environment {
        sonarUrl = 'sonar.host.url=http://172.17.0.3:9000'
	    sonarToken = "sonar.login=${SonarToken}"
	    scannerHome = tool 'sonar_scanner'
    }
 
 stages {
  
     stage('MvnPackage'){
	 // Build using maven
	   //Get Maven Home Path
	   steps { 
	     sh 'mvn clean package -DskipTest=true'
	   }  
    }
	 
	 
     stage( 'Teste Unitario') {
	 steps { 
	   junit allowEmptyResults: true, testResults: 'target/surefire-reports/*.xml'
	   sh 'mvn clean jacoco:prepare-agent install'
           sh 'mvn jacoco:report'
	 }
    } 
	 
   
     stage( 'Scanner sonar') {
        steps{
        	//sh "${mvn} sonar:sonar -D${sonarUrl}  -D${sonarToken}"
                //sh "mvn sonar:sonar -D${sonarUrl} -Dsonar.login=a5e73b0104116d3c3d30840822f94a896c568a6d"
		withSonarQubeEnv('sonar_server'){
                sh "${scannerHome}/bin/sonar-scanner -Dsonar.projectKey=DevopsLAB -Dsonar.java.binaries=target -Dsonar.coverage.exclusions=**/mvm**,**/src/test/**,**/model/** -Dsonar.junit.reportPath=target/surefire-reports" 
                }
          }
      }
      
}

	post ( 'Check Quality Gate') { 
        	always {     
                steps{
		    withSonarQubeEnv('sonar_server'){
                    //script {
    			        qg = waitForQualityGate() // Reuse taskId previously collected by withSonarQubeEnv
    			        if (qg.status != 'OK') {
							error "Pipeline aborted due to quality gate failure: ${qg.status}"
                    }
    			    }
  			    }

		    //}
		    }
	}

}
