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
  stage('Publish Results'){
      steps{
    junit 'gameoflife-web/target/surefire-reports/*.xml' , archive 'gameoflife-web/target/*.war'
	}
	}
	}
	
	post {
	success {
	emailext(emailext body: 'Build_3.5V Success', recipientProviders: [developers()], subject: 'Build_3.5V Success', to: 'baji.g@ecartag.com')
	}
	Faiure {
	emailext(emailext body: 'Build_3.5V Faile', recipientProviders: [developers()], subject: 'Build_3.5V Faile', to: 'baji.g@ecartag.com')
	}
	}
	}
	
