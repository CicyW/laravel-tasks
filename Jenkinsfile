pipeline {
    agent any

    stages {
        stage("Environment Check") {
            steps {
                echo "environment checking ..."
                sh 'php --version'
                sh 'composer --version'
                sh 'npm --version'
                sh 'mysql --version'
                echo "environment check done."
            }
        }

        stage("Build") {
            steps {
                echo "Buliding..."
                sh 'composer update'
                sh 'composer install -n --ignore-platform-reqs'
                echo "Build done."
            }
        }

        Stage("Deploy") {
            steps {
                echo "Deploying..."
                sh 'php artisan key:generate --force'
                sh 'sudo cp -r ./ /var/www/php'
                sh 'sudo chown -R www-data:www-data /var/www/php'
                sh 'sudo chmod -R 775 /var/www/php/storage'
                sh 'sudo service apache2 restart'
                echo "Deploy done..."
            }
        }

    }

    post {
        aborted {
            script {
                currentBuild.result = 'SUCCESS'
            }
        }
    }

}
