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

        post {
        success {
            jacoco(
                execPattern: '**/build/jacoco/*.exec',
                classPattern: '**/build/classes/java/main',
                sourcePattern: '**/src/main'
            )
        }
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
