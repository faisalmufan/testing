pipeline {
    agent any

    environment {
        // Set up environment variables if necessary
        PHP_VERSION = '8.3'
        COMPOSER_HOME = '/var/www/.composer'
    }

    stages {
        stage('checking code'){
            when{
                branch 'develop'
            }
        }

        stage('Deploy') {
            when {
                branch 'develop'
            }
            steps {
                sshPublisher(publishers: [sshPublisherDesc(configName: 'prod-test', transfers: [sshTransfer(cleanRemote: false, excludes: '', execCommand: '', execTimeout: 120000, flatten: false, makeEmptyDirs: false, noDefaultExcludes: false, patternSeparator: '[, ]+', remoteDirectory: '/var/www/html/', remoteDirectorySDF: false, removePrefix: '', sourceFiles: '.')], usePromotionTimestamp: false, useWorkspaceInPromotion: false, verbose: false)]) 
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
