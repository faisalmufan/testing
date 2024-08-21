pipeline {
    agent any

    environment {
        // Set up environment variables if necessary
        PHP_VERSION = '8.3'
        COMPOSER_HOME = '/var/www/.composer'
    }

    stages {

        stage('Deploy') {
            when {
                branch 'develop'
            }
            steps {
                script {
                    // Deploy the code to the server
                    // Example: Using rsync to deploy to the server
                    sshagent(['ssh-root']) {
                        sh 'sudo apt update'
                    } 
                }
            }
        }
    }

    post {
        always {
            // Cleanup steps, notifications, etc.
            echo 'Pipeline completed!'
        }

        success {
            echo 'Build was successful!'
        }

        failure {
            echo 'Build failed!'
        }

        cleanup {
            // Optional: Delete any temporary files or directories
            deleteDir()
        }
    }
}
