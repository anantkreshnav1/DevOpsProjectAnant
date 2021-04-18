pipeline {

  agent any

  stages {
    
    //Github Checkout
    
     stage ('Clone Repo') {
            steps {
                /* Clone git Repository */
                checkout scm
                   }
                              }

    //Docker Image Building
    
     stage('Building image') {
        steps{
          script {
              //sh "docker build -t ramktcs/phpapp-3 ."
        app = docker.build("anantkreshnav/phpapp")
          }
      }
    }

    //Docker Image push to Dockerhub
    
   stage ('Push Image') {
     steps  {
          echo "Push Image on DockerHub"
          script {
                    docker.withRegistry('https://registry.hub.docker.com', 'dockerhub')
               
            
            {            
       app.push("${env.BUILD_NUMBER}")            
       app.push("latest")        
              }    
            
}
}
}
    
      //Docker Image deployment
    
    stage ('Deploy') {
     steps {
         echo "Run containers"
         script {
          sh "docker run -d -p 8081:80 anantkreshnav/phpapp"
                     }
                  }
  }          
    

  }
}
