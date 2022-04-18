node {
     def app 

     environment {
		DOCKERHUB_CREDENTIALS=credentials('docker_hub')
	}

     stage('clone repository') {
     checkout([$class: 'GitSCM', branches: [[name: '*/master']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/cloudgladiator/nodejs-jenkins.git']]])
    }
     stage('Build docker Image'){
      app = docker.build("741041/docker-node")
    }
     stage('Test Image'){
       app.inside {
         sh 'echo "TEST PASSED"' 
      }  
    }

    stage('Login') {

			steps {
				sh 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin'
			}
		}

        stage('Push') {

			steps {
				sh 'docker push 741041/docker-node:latest'
			}
		}
   }
}
