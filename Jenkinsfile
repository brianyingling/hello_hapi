#!/usr/bin/env groovy

pipeline {

    agent {
        docker {
            image 'node'
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
                withDockerRegistry('docker-hub-credentials') {
                    sh "docker push brianyingling/orsty:latest"
                }
            }
        }
    }
}
