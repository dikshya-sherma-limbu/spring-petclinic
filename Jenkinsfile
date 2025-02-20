pipeline {
    agent any

    triggers {
        cron('H/3 * * * 4') // Triggers every 3 minutes on Thursdays
    }

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/dikshya-sherma-limbu/spring-petclinic.git'
            }
        }

        stage('Build') {
            steps {
                bat 'mvnw.cmd clean package' // Use bat for Windows
            }
        }

        stage('Code Coverage with JaCoCo') {
            steps {
                bat 'mvnw.cmd test jacoco:report' // Use bat for Windows
            }
            post {
                always {
                    junit '**/target/surefire-reports/*.xml'
                    jacoco execPattern: '**/target/jacoco.exec'
                }
            }
        }
    }

    post {
        success {
            echo 'Pipeline completed successfully!'
        }
        failure {
            echo 'Pipeline failed!'
        }
    }
}
