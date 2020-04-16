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
                sh 'php artisan key:generate --env=production --force'
                sh 'php artisan migrate --env=production --force'
                sh 'php artisan serve --env=production --port=8080 &'
                echo "Build done."
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
