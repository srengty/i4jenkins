pipeline {
    agent any
    tools {
        jdk 'jdk21'
        maven 'maven'
    }

    stages {
        stage('Fetch code') {
            steps {
                git branch: 'main', url:'https://github.com/srengty/i4jenkins.git'
            }
        }
        
        stage('Build') {
            steps {
                sh 'mvn clean install -DskipTests'
            }
            post {
                success {
                    echo 'Now Archiving...'
                    archiveArtifaces artifacts: '**/*.jar'
                }
            }
        }
        stage('Test') {
            steps {
                sh 'mvn test'
            }
        }
        stage('Checkstyle analysis') {
            steps {
                sh 'mvn checkstyle:checkstyle'
            }
        }
    }
}