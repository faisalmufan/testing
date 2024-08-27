pipeline{
    agent any 
    triggers {
        upstream 'develop, '
        }
    stages{
        stage('checking code'){
            steps{
              echo "checking code"
              sh 'composer install'
            }
        }
        stage('testing code'){
            when{
                branch 'develop'
                beforeOptions true
                // beforeInput true
            }
             steps{
                sh 'composer require --dev mds-agenturgruppe/php-code-checker:^3.0'
                sh 'vendor/bin/mds-code-check'
                
            }
            input {
                message 'apakah sudah selesai di testing '
                id '11'
                ok 'yes'
                }
        }

        stage('deploy code'){
            when{
                branch 'main'
                beforeInput true
            }
             input {
                message 'sudah yakin untuk deploy '
                id '12'
                ok 'yes'
                }
            steps{
                script{
                    sshagent(credentials: ['ssh-wisnu'], ignoreMissing: true) {
                        sh 'rsync -avz  ./ wisnu@192.168.23.78:/home/wisnu/jenkins'
                    }
                }
            }
        }

    }
}