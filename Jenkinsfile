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
    }
    node {
        def image = docker.build("brianyingling/hello_hapi:${env.BUILD_ID}")
        docker.withRegistry('https://registry.hub.docker.com', 'docker-hub-credentials') {
            image.push('latest')
        }
    }
}
