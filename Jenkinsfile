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
            steps{
                sh './vendor/bin/phpinit'
                input{
                    message "Apakah tidak ada bug atau error ?"
                    id "simple-input"
                }
            }
        }

        stage('deploy code'){
            when{
                branch 'main'
                beforeInput true
            }
            sshagent(credentials: ['ssh-wisnu'], ignoreMissing: true) {
                sh 'rsync -avz ./ wisnu@192.168.23.78:/home/wisnu/'
            }
        }

    }
}