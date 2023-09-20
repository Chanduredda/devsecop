pipeline {
    agent any


stages {

    stage('Build Artifact - Maven') {
        steps {
            sh "mvn clean package -DskipTests=true"
            archive 'target/*.jar'
        }
        }

        stage('Unit Tests - JUnit and JaCoCo') {
        steps {
            sh "mvn test"
            
        }
         
        }

        stage('Mutation Tests - PIT') {
        steps {
            sh "mvn org.pitest:pitest-maven:mutationCoverage"
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


