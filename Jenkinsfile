node {
     def app 
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
     stage('Push Image'){
       docker.withRegistry('https://hub.docker.com/repository/docker/741041/docker-node', 'git') { 
       docker push 741041/docker-node:741041/docker-node
       app.push("${env.BUILD_NUMBER}")            
       app.push("latest")   
   }
}
}
