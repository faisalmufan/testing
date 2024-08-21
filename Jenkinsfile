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
                // script {
                //     // Deploy the code to the server
                //     // Example: Using rsync to deploy to the server
                //     // echo 'rsync -avz --exclude="*.env" ./ user@server:/path/to/deploy/'
                // }

                sshPublisher(publishers: [sshPublisherDesc(configName: 'prod-test', transfers: [sshTransfer(cleanRemote: false, excludes: '', execCommand: 'sudo composer update', execTimeout: 120000, flatten: false, makeEmptyDirs: false, noDefaultExcludes: false, patternSeparator: '[, ]+', remoteDirectory: '/var/www/html/$BUILD_NUMBER', remoteDirectorySDF: false, removePrefix: '', sourceFiles: '/var/www/html')], usePromotionTimestamp: false, useWorkspaceInPromotion: false, verbose: false)]
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
