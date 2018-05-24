#!/usr/bin/env groovy

pipeline {

    agent {
        docker {
            image 'node:9'
            args '-u root'
        }
    }

    stages {
        stage('Build') {
            steps {
                echo 'Building...'
                sh 'npm install'
            }
        }
        stage('Test') {
            steps {
                echo 'Testing...'
                sh 'npm test'
            }
        }
        stage('Publish') {
            steps {
                withDockerRegistry([credentialsId: 'docker-hub-credentials', url: '']) {
                    sh "docker push brianyingling/orsty:latest"
                }
            }
        }
    }
}
