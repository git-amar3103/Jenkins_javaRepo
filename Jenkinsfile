
pipeline {
    agent any

    tools {
        jdk 'JDK21'
        maven 'Maven3'
    }

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main',
                    url: 'https://github.com/git-amar3103/Jenkins_javaRepo.git'
            }
        }

        stage('Verify Tools') {
            steps {
                sh 'java -version'
                sh 'mvn -version'
                sh 'ls -l pom.xml'
            }
        }

        stage('Build and Package') {
            steps {
                sh 'mvn clean package'
            }
        }

        stage('Test Results') {
            steps {
                junit allowEmptyResults: true,
                      testResults: '**/target/surefire-reports/*.xml'
            }
        }

        stage('Archive JAR') {
            steps {
                archiveArtifacts(
                    artifacts: '**/target/*.jar',
                    fingerprint: true,
                    allowEmptyArchive: false
                )
            }
        }
    }

    post {
        success {
            echo 'Build successful. Check the archived artifact.'
        }
        failure {
            echo 'Build failed. Review Console Output.'
        }
    }
}
