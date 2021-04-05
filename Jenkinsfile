pipeline 
{

 agent 
  {
   label 'MAVEN'
   }
     
  stages
  {
  stage ('Pull the Repo'){
    steps
	{
	git credentialsId: 'ServiceAccount1', url: 'https://github.com/wakaleo/game-of-life.git'
    }
	}
  stage('Build'){
    steps {
	 sh 'mvn package'
	 }
	 }
  stage('Publish Results'){
      steps{
    junit 'gameoflife-web/target/surefire-reports/*.xml' , archive 'gameoflife-web/target/*.war'
	}
	}
	}
	
	post {
	success {
	emailext(subject: "${env.JOB_NAME} [${env.BUILD_NUMBER}] Development Promoted to Master",
            body: """<p>'${env.JOB_NAME} [${env.BUILD_NUMBER}]' Development Promoted to Master":</p>
            <p>Check console output at &QUOT;<a href='${env.BUILD_URL}'>${env.JOB_NAME} [${env.BUILD_NUMBER}]</a>&QUOT;</p>""",to: 'baji.g@ecartag.com')
	}
	failure {
	emailext( subject: "${env.JOB_NAME} [${env.BUILD_NUMBER}] Failed!",
            body: """<p>'${env.JOB_NAME} [${env.BUILD_NUMBER}]' Failed!":</p>
            <p>Check console output at &QUOT;<a href='${env.BUILD_URL}'>${env.JOB_NAME} [${env.BUILD_NUMBER}]</a>&QUOT;</p>""", to: 'baji.g@ecartag.com')
	}
	}
	}
	
