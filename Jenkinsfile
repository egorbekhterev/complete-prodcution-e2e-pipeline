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
        stage("Sonarqube analysis") {
            steps {
                script {
                    withSonarQubeEnv(credentialsId: 'jenkins-sonarqube-token') {
                        sh "mvn sonar:sonar"
                    }
                }
            }
        }
        stage("Quality Gate") {
            steps {
                script {
                    waitForQualityGate abortPipeline: false, credentialsId:  'jenkins-sonarqube-token'
                }
            }
        }
    }
}
