@Library ("Shared") _
pipeline {
    agent { label 'jenkins-worker-1' }
    stages{
        
        stage ("Call github library")
        {
            steps{
                script {
                    hello()
                    
                }
            }
        }
    
    stage ('Project clone')
    {
        steps{
            script 
            {
                gitclone ("https://github.com/immortalRajput/webapp.git" , "master")
            }
            
           // git branch: 'master' , url: 'https://github.com/immortalRajput/webapp.git'
            
        }
    }
       
    stage ('Create docker image')
    {
        steps{
          sh  " docker build -t krytox/webapp:latest . "
        // sh "docker run -d -p 82:80 --name mywebapp webapp:v1"
        }
    }
   stage('Docker Login & Push') {
    steps {
        withCredentials([usernamePassword(credentialsId: 'dockerhubcred', usernameVariable: 'dockerHubUser', passwordVariable: 'dockerHubPass')]) {
            sh """
                echo "Logging in to Docker Hub..."
                docker login -u $dockerHubUser -p $dockerHubPass
                echo "Pushing Docker image..."
                docker push krytox/webapp:latest
            """
        }
    }
}

    
    stage ('Run the image to container')
    {
        steps {
         sh "docker images"
        }
    }
    
}
}
