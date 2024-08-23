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
            input{
                    message "Apakah tidak ada bug atau error ?"
                    id "simple-input"
                }
            steps{
                sh './vendor/bin/phpinit'
                
            }
        }

        stage('deploy code'){
            when{
                branch 'main'
                beforeInput true
            }
            script{
                sshagent(credentials: ['ssh-wisnu'], ignoreMissing: true) {
                    sh 'rsync -avz ./ wisnu@192.168.23.78:/home/wisnu/'
                }
            }
        }

    }
}