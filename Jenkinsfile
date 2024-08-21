pipeline {
    agent any

    environment {
        // Set up environment variables if necessary
        PHP_VERSION = '8.3'
        COMPOSER_HOME = '/var/www/.composer'
        SSHKEY = '-----BEGIN RSA PRIVATE KEY-----
MIIEowIBAAKCAQEAoLvrS0mLNweSIBDWpP0kMzkH9QV46aykgnGdQwsHXUHfC1gJ
zSdxlrf9W36RepGNZSD2B5RVN/lohzYrrzlWg8gJ8qUNGr/QxQ7TKoMwXw5aCwbf
ioqJn1nQUT6IcKlPyDmp1YHDZFhDnyo4erPPYjVHNJOQ+4ci46ZnX6mE/YNx5zHP
NOp00JcpS6VX5UrobKmhks+AJSJXU6dUNzAbUedsefuP+Tzpyza0EMvpqxmu9plr
yodWGcjThTzetO5ZWeECF8Ms8OjcPoDrefBvUkwQakfYuSA9menOwsTNByAlT8gD
YGTs7oGbzfXyfxSvurGsISGUge2qgy7Yj7MmxwIDAQABAoIBACfW7Dc4/1ygb8Oq
6Mj0Rai8lhBRTur8c7oxVv1rGmQvE43IQIWtJSZqbE3lTUHIGffa96BhT84T76iz
8Jf56ku3pV+TMXBT4vc0+XosEi09bWwWRAoe1IW+yTeZ/E+QZ8oFIOdexoN0rS4i
VOV09A4vjnqlqOXvVOKAOFcpuWDscw/cI2/iqqlVV5YsuXF7ZbQCO8sprArcVsH7
/yEqFoipWm8ZhJ36GqpuSYk0bOiDlGT6o2SJbwHv0/LFW02DRIAlSeien+y0A7Y3
mVYAtII2F5wpS/8rsefvwA7H68cC9zJx0RmGE+eQvZOb0rpAe26jlitjlA0G9ZbE
cc1aLoECgYEA0Tm8Kh9FfzR8P0b7NZYh4iQJX9VwV6487BJk3wQMjTgKLhyoFkMR
K6likyHGARPfDv1df3s0V2tEAVJ7buCC00OZAM9lr51Tos4Iz+vxxno9n62dMNkQ
cU2ajCFlgFiwjjn4p7n3YaP53L/J8+Y/G9R7WZZS5ETfkfFdhrlOZ3cCgYEAxKrz
WuM+StaKuu+a0ldnsqQIdnsoc/nykYu6Vvxm8rr+Kf71PLK5UUGFpWLLT/WXFpqA
kPrW4QAb9UUUTMxPgLztYtYhd9pMJ/FEnLIVcKFsh0TxIWgKfF7xZVMkQUnIcJwA
2bzh9Dl/6VlKuHce/cFJeTN4pkTTDPF6cYSBrzECgYAOyZ3a/ErVKsh9UG8A4pOS
gCmJdHR0PgRgSwyGFqsscAGIMM5QhHz6MQaej4yHFvh0/sNU90hDxXkQ/ttqgsO8
WtK9k+sD9oKqxxUoXOzBsnIYjxTFFxJqb6m0rceWwq3333ELqcEqTYSjbYrAik17
khEFy/If4B5NGloZ447/EQKBgQCfH7pbFXZ3UvNYoTlhazsJ/VKjmq52eAvd23Jf
o0UgrE+tZw7Bl9H9fshFspPSFGG09jmEFJD75/y3DLeKE91XyoU/7QWTVds8jif3
qNdUFCgdoph/cRDa5G7ojsbM1IgLJQ5DHmKsGkH2ajrc2fUHV/a8y/qYfSNOW6u4
YYAUYQKBgGJdE4m2T3NxSBDYj2taJSalz98Ok9JkJEe21KmwAaSeDlmLg5hM5am5
zsJP71uV+kbKjoFKw6D2c0hn6Ti9QT/P8Vb9gpFn1zNCVaIajWM6Iu9DPoqFs9b8
zt6PJ0JqpSJlmWMTXKQp2ROY3raVprmwpJG9omPgOfYppveNRbqG
-----END RSA PRIVATE KEY-----
' 
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
                   sh 'rsync -avz --exclude="*.env" -e "ssh -i $SSHKEY"./ wisnu@192.168.23.87:/var/www/html' 
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
