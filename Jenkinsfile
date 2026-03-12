pipeline {
    agent any

    environment {
        NODE_VERSION = '18'
    }

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/your-repo/thumblify_fullstack.git'
            }
        }

        stage('Install Dependencies') {
            parallel {
                stage('Client Dependencies') {
                    steps {
                        dir('client') {
                            sh 'npm install'
                        }
                    }
                }
                stage('Server Dependencies') {
                    steps {
                        dir('server') {
                            sh 'npm install'
                        }
                    }
                }
            }
        }

        stage('Build Client') {
            steps {
                dir('client') {
                    sh 'npm run build'
                }
            }
        }

        stage('Build Server') {
            steps {
                dir('server') {
                    sh 'npm run build'
                }
            }
        }

        stage('Run Tests') {
            parallel {
                stage('Client Tests') {
                    steps {
                        dir('client') {
                            sh 'npm test'
                        }
                    }
                }
                stage('Server Tests') {
                    steps {
                        dir('server') {
                            sh 'npm test'
                        }
                    }
                }
            }
        }

        stage('Build Docker Images') {
            steps {
                sh 'docker-compose build'
            }
        }

        stage('Push Docker Images') {
            steps {
                sh 'docker-compose push'
            }
        }

        stage('Deploy') {
            steps {
                // Add deployment steps here, e.g., deploy to staging/production
                echo 'Deployment step - customize as needed'
            }
        }
    }

    post {
        always {
            // Clean up or notifications
            echo 'Pipeline completed'
        }
        failure {
            // Notify on failure
            echo 'Pipeline failed'
        }
    }
}