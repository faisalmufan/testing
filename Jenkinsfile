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
                    message 'apakah sudah selai di testing ??'
                    id 'id-massage'
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