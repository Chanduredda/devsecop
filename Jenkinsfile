    pipeline {
        agent any 

        stages {
            steps('checkout') {
                steps {
                        sh "mvn clean package -DskipTests=true"//Adding comment//
                        archive 'target/*.jar'
              }
            }
        }
    }