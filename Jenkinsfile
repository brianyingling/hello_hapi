#!/usr/bin/env groovy

pipeline {

    agent {
        docker {
            image 'node'
            args '-u root'
        }
    }

    stages {
        stage('Pre') {
            steps {
                sh 'node --version'
                sh 'docker --version'
            }
        }
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
                docker.withRegistry([credentialsId: 'docker-hub-credentials', url: '']) {
                    def image = docker.build("hello_hapi:${env.BUILD_ID}")
                    image.push()
                }
            }
        }
    }
}
