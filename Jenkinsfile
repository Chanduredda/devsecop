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

      stage('Docker image build and push') {
      steps {
        sh 'printenv'
         withDockerRegistry([credentialsId: "docker-hub", url: ""]){
        sh 'docker build -t devsecops89:5000/java-app:latest'
        sh 'docker push devsecops89/numeric-app:5000/java-app:latest'
         }
        
       }
     }

  //   stage('Push to Docker Hub') {
  //           steps {
  //               // Log in to Docker Hub with credentials from Jenkins
  //               withCredentials([usernamePassword(credentialsId: 'ZGV2c2Vjb3BzODk6S2FydGhpS2V5YSNAMTc=', usernameVariable: 'devsecops89', passwordVariable: 'KarthiKeya#@17')]) {
  //               script {
  //                   // Use sh to pass the password securely to docker login
  //                   sh 'echo $DOCKER_PASSWORD | docker login -u $DOCKER_USERNAME --password-stdin'
  //               }
            
  //           // Push the Docker images to Docker Hub
  //           sh 'docker-compose push'
  //               }
  //           }
  
  //  }


// stage('Docker image build and push') {
//     steps {
//         script {
//             // Define your Docker registry credentials ID and URL
//             def registryCredentials = 'devsecops89'
//             def registryUrl = 'https://hub.docker.com/repository/docker/devsecops89'

//             // Configure Docker registry with credentials
//             withDockerRegistry([credentialsId: registryCredentials, url: registryUrl]) {

//                 // Specify Dockerfile path and build context
//                 def dockerfile = '/root/.docker'
//                 def buildContext = '/root/.docker'

//                 // Define the image name and tag
//                 def imageName = 'devsecops89:5000/java-app:latest'

//                 // Build the Docker image
//                 sh "docker build -t ${imageName} -f ${dockerfile} ${buildContext}"

//                 // Push the Docker image
//                 sh "docker push ${imageName}"
//             }
//         }
//     }
// }


 }

}

 


