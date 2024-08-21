pipeline {
    agent any

    environment {
        // Set up environment variables if necessary
        PHP_VERSION = '8.2'
        COMPOSER_HOME = '/var/www/.composer'
    }

    stages {
        // stage('Checkout') {
        //     steps {
        //         // Checkout the code from the repository
        //         git branch: 'main', url: 'https://your-repo-url.git'
        //     }
        // }

        stage('Install Dependencies') {
            steps {
                script {
                    // Ensure Composer is installed
                    sh 'composer install --prefer-dist --no-interaction --optimize-autoloader --no-suggest'
                }
            }
        }

        stage('Static Analysis') {
            steps {
                script {
                    // Run PHPStan or another static analysis tool
                    sh 'vendor/bin/phpstan analyse'
                }
            }
        }

        stage('Code Style Check') {
            steps {
                script {
                    // Run PHP CodeSniffer for coding standards
                    sh 'vendor/bin/phpcs --standard=PSR12 src/'
                }
            }
        }

        stage('Run Unit Tests') {
            steps {
                script {
                    // Run PHPUnit tests
                    sh 'vendor/bin/phpunit --coverage-text --colors=always'
                }
            }
        }

        stage('Build') {
            steps {
                script {
                    // Build the application (e.g., optimize autoloader)
                    sh 'composer dump-autoload -o'
                }
            }
        }

        stage('Security Checks') {
            steps {
                script {
                    // Run security analysis with tools like PHP Security Checker
                    sh 'vendor/bin/php-security-checker'
                }
            }
        }

        stage('Deploy') {
            when {
                branch 'main'
            }
            steps {
                script {
                    // Deploy the code to the server
                    // Example: Using rsync to deploy to the server
                    sh 'rsync -avz --exclude="*.env" ./ user@server:/path/to/deploy/'
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
