pipeline {
  agent any

  stages {

    stage('Build Artifact - Maven') {
      steps {
        sh "mvn clean package -DskipTests=true"
        archive 'target/*.jar'
      }
    }

    stage('Unit Tests - JUnit and Jacoco') {
      steps {
        sh "mvn test"
      }
      post {
        always {
          junit 'target/surefire-reports/*.xml'
          jacoco execPattern: 'target/jacoco.exec'
        }
      }
    }

    //   stage('Docker image build and push') {
    //   steps {
    //      withDockerRegistry([credentialsId: "docker-hub", url: ""]){
    //     sh 'docker build -t devsecops89:5000/java-app:latest'
    //     sh 'docker push devsecops89/devsecops:5000/java-app:latest'
    //      }
        
    //    }
    //  }

    stage('Push to Docker Hub') {
            steps {
                // Log in to Docker Hub with credentials from Jenkins
                withCredentials([usernamePassword(credentialsId: 'docker-hub-credentials', usernameVariable: 'devsecops89', passwordVariable: 'KarthiKeya#@17')]) {
                script {
                    // Use sh to pass the password securely to docker login
                    sh 'echo $DOCKER_PASSWORD | docker login -u $DOCKER_USERNAME --password-stdin'
                }
            
            // Push the Docker images to Docker Hub
            sh 'docker-compose push'
                }
            }
  
   }
 }

}

 


