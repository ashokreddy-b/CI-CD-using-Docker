pipeline {
    agent any

 stages {
	 
      stage('checkout') {
           steps {
             
                git branch: 'master', url: 'https://github.com/devops4solutions/CI-CD-using-Docker.git'
             
          }
        }
	stage('Package and Build App') {
      steps {
        echo 'Build and Package App'
        sh 'mvn clean package'
           }
   	 }

stage('Image creation') {
      steps {
        sh 'docker build -t bapathuashokreddy/samplewebapp .'
                    }
            }

stage('Docker Login') {
      steps {
	  withCredentials([usernamePassword(credentialsId: 'Docker', passwordVariable: 'pwd', usernameVariable: 'user')]) {
      sh "docker login -u ${env.user} -p ${env.pwd}"
}	
            }
      }

 stage('Push Image to Docker Registry') {
      steps {
        sh 'docker push bapathuashokreddy/samplewebapp'
            }
           }
     
      stage('Run Docker container on Jenkins Agent') {
             
            steps{
                sh "docker run -d -p 8003:8080 bapathuashokreddy/samplewebapp"
 
            }
        }
    }
	}
    
