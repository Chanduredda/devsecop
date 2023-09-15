pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                    sh "mvn clean package -DskipTests=true"//Adding comment//
                    archive 'target/*.jar'
            }
        }

         stage('Unit Tests - JUnit and JaCoCo') {
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

               stage('Docker Build and Push') {
                  steps {
                    withDockerRegistry([credentialsId: "docker-hub", url: ""]) {
                    sh 'printenv'
              sh 'sudo docker build -t chandrareddya/devsecops:""$GIT_COMMIT"" .'
              sh 'docker push chandrareddya/devsecops:""$GIT_COMMIT""'
                    }
                  }
              }



          }
      }