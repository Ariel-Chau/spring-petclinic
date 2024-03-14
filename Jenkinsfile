pipeline {
    agent any

    tools {
        maven "MAVEN3" 
    }

    stage('Cloning git') {
            steps {
                 git branch: 'main', url: 'https://github.com/Ariel-Chau/spring-petclinic'
            }
        }

    stages {
        stage('Checkout and Build') {
            steps {

                git branch: 'master', url: 'https://github.com/Ariel-Chau/spring-petclinic'
    
                bat "mvn clean org.jacoco:jacoco-maven-plugin:prepare-agent package"
            }
            post {
                success {
                    
                    junit '/target/surefire-reports/TEST-*.xml'
                    archiveArtifacts 'target/*.jar'
                }
            }
        }
        
        stage("Code Coverage") {
            steps {
                script {

                    bat "mvn org.jacoco:jacoco-maven-plugin:report"

                    jacoco(execPattern: 'target/jacoco.exec')
                }
            }
        }
        
    
    }
}