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

     }

     }
}