pipeline {
    agent any

    tools {
        jdk 'jdk11'       // Name from Jenkins Global Tool Configuration
        maven 'maven3'    // Name from Jenkins Global Tool Configuration
    }

    environment {
        JAVA_HOME = "${tool 'jdk11'}"
        PATH = "${JAVA_HOME}/bin:${env.PATH}"
        MAVEN_HOME = "${tool 'maven3'}"
    }

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/SriBoo/spring-petclinic.git'
            }
        }

        stage('Build') {
            steps {
                sh 'mvn clean install'
            }
        }

        stage('Test') {
            steps {
                sh 'mvn test'
            }
        }

        stage('Package') {
            steps {
                sh 'mvn package'
            }
        }

        stage('Archive JAR') {
            steps {
                archiveArtifacts artifacts: 'target/*.jar', fingerprint: true
            }
        }
    }
}
