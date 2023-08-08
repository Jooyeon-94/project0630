pipeline{
  agent {
    label "node1"
  }    
	stages{
    	stage('Prepare') {
    	    steps{
    		    script{
    		    	cleanWs()
    		    	pwd = sh(script: "pwd", returnStdout:true).trim()
    			    sh """
    			    	git clone https://github.com/Jooyeon-94/project0630.git
    			    	cd ${pwd} ./gradlew clean build -x test
    			    """
    		    }    	                  
    	    }
    	}		
    	stage('API Test') {
    		steps{
    			script{
    				try{
    					sh "newman run ${pwd}/project0630/Test_pass.postman_collection.json --reporters cli,junit --reporter-junit-export 'newman/NEWMAN-myreport.xml'"   				
    				}catch(err){
    					println("test error : ${err}")
    					sh "exit 0"
    				}		
    			}
			}           	
    	}	
    	stage('Result') {
    		steps{
    			junit '**/newman/NEWMAN-myreport.xml'
    		}           	
    	}	
	}
}

