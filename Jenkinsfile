pipeline {
    agent any
    tools {
        jdk 'Java17'
        maven 'Maven3'
    }
    stages {
        stage("Cleanup workspace") {
            steps {
                cleanWs()
            }
        }
        stage("Checkout for SCM") {
            steps {
                git branch: 'main', credentialsId: 'github', url: 'https://github.com/egorbekhterev/complete-prodcution-e2e-pipeline'
            }
        }
        stage("Build application") {
            steps {
                sh "mvn clean package"
            }
        }
        stage("Test application") {
            steps {
                sh "mvn test"
            }
        }
    }
}