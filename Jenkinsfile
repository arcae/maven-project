pipeline {
	agent any
        parameters{
            string(name: 'tomcat_dev',defaultValue: '34.229.204.115',description: 'Staging server')
        }
        
        triggers {
            pollSCM('* * * * *')
        }
	stages
        {
		stage('Build'){
		    steps {
		       sh 'mvn clean package' 
		    }
            post{
               success{
                   echo 'Now Archiving.....'
                   archiveArtifacts artifacts: '**/target/*.war'
                 }
            }
        }  
	    stage('Deploy to Staging'){
	        steps{
	            sh "scp -o "StrictHostKeyChecking=no" -i /home/regi/MyEC2Virginia.pem **/target/*.war ec2-user@${params.tomcat_dev}:/var/lib/tomcat/webapps"

	        }
	    }

	}
}
