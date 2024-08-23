pipeline{
    agent any 
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
            input {
                message 'halo guys'
                id '11'
                ok 'yes'
                }
            steps{
                sh 'phpunit --log-junit test-results.xml'
                
            }
        }

        stage('deploy code'){
            when{
                branch 'main'
                beforeInput true
            }
            steps{
                script{
                    sshagent(credentials: ['ssh-wisnu'], ignoreMissing: true) {
                        sh 'rsync -avz ./ wisnu@192.168.23.78:/home/wisnu/'
                    }
                }
            }
        }

    }
}