pipeline {
    agent any
    
    stages{
        
        stage('git clone'){
            
            steps{
                git 'https://github.com/githubu.name/reponame'
            }
        }
        
        stage('Build'){
            
            steps{
                sh 'mvn package'
				
            }
		
        }
	
        stage('sonar analysis'){
		
	    steps{
	        withSonarQubeEnv('sonar') {
                sh 'mvn sonar:sonar'
              }
	    }
        }
		
        
        stage('copy war to petwar dir'){
            
            steps{
                sh 'sudo cp /var/lib/jenkins/workspace/sample_test/target/*.war /root/petwar'
            }
        }
        
        stage('post build actions'){
            
            steps{
                archiveArtifacts 'target/petclinic.war'
            }
        }
        
        stage('JUnit test results'){
            
            steps{
                junit 'target/surefire-reports/*.xml'
            }
        }
		
        
        stage('jfrog'){
            
            steps{
                script{
                    def SERVER_ID = 'jfrog'
                    def server = Artifactory.server SERVER_ID
                    
                    def uploadSpec = """{
                        "files": [{
                                    "pattern": "**/*.war",
                                    "target": "pet"
                        }]
                    }"""
                    
                    server.upload(uploadSpec)
                }
            }
        }
    }
}
