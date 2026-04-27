pipeline {
    agent none 

    stages {
        stage('Parallel dynamic agents') {
            parallel {
                stage('Build (Python)') {
                    agent {
                        docker {
                            image 'python:3.11-slim'
                            label 'docker-agent'
                            args '-v /var/run/docker.sock:/var/run/docker.sock'
                        }
                    }
                    steps {
                        sh 'hostname'
                        sh 'python3 --version'
                        sh 'pip install --quiet pytest'
                        sh 'pytest --version'
                    }
                }

                stage('Tools (Node)') {
                    agent {
                        docker {
                            image 'node:20-slim'
                            label 'docker-agent'
                            args '-v /var/run/docker.sock:/var/run/docker.sock'
                        }
                    }
                    steps {
                        sh 'hostname'
                        sh 'node --version'
                        sh 'npm --version'
                    }
                }
            }
        }
    }
}
