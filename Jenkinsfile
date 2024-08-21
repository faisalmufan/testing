pipeline {
    agent any

    environment {
        PHP_VERSION = '8.2'
        COMPOSER_HOME = '/var/www/.composer'
    }

    stages {

        stage('Install Dependencies') {
            steps {
                sh 'composer install --prefer-dist --no-interaction --optimize-autoloader --no-suggest'
            }
        }

        stage('Static Analysis') {
            when {
                expression {
                    return env.BRANCH_NAME == 'main' || env.BRANCH_NAME.startsWith('feature/')
                }
            }
            steps {
                sh 'vendor/bin/phpstan analyse'
            }
        }

        stage('Code Style Check') {
            when {
                expression {
                    return env.BRANCH_NAME == 'main' || env.BRANCH_NAME.startsWith('feature/')
                }
            }
            steps {
                sh 'vendor/bin/phpcs --standard=PSR12 src/'
            }
        }

        stage('Run Unit Tests') {
            steps {
                sh 'vendor/bin/phpunit --coverage-text --colors=always'
            }
        }

        stage('Build') {
            steps {
                sh 'composer dump-autoload -o'
            }
        }

        stage('Deploy to Staging') {
            when {
                branch 'develop'
            }
            steps {
                sh 'rsync -avz ./ user@staging-server:/path/to/staging/deploy/'
            }
        }

        stage('Deploy to Production') {
            when {
                branch 'main'
            }
            steps {
                sh 'rsync -avz ./ user@production-server:/path/to/production/deploy/'
            }
        }
    }

    post {
        always {
            echo 'Pipeline completed!'
        }

        success {
            echo 'Build was successful!'
        }

        failure {
            echo 'Build failed!'
        }

        cleanup {
            deleteDir()
        }
    }
}
