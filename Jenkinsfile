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
         post {
        always {
            
            junit 'target/surefire-reports/*XML'
            jacoco execPattern: 'target/jaccoco.exec'
            
        }
    }
     }

        stage('Mutation Tests - PIT') {
        steps {
            sh "mvn org.pitest:pitest-maven:mutationCoverage"
        }
    
     }
    
    }

}
