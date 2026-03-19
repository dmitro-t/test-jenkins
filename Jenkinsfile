pipeline {
    agent any

    stages {
        stage('Install Apache') {
            steps {
                echo 'Installing Apache Server...'
                sh 'sudo apt-get update'
                sh 'sudo apt-get install -y apache2'
                sh 'sudo systemctl start apache2'
                sh 'sudo systemctl enable apache2'
            }
        }

        stage('Check Logs') {
            steps {
                echo 'Checking logs for 4xx and 5xx errors...'
                script {
                    def logFile = "/var/log/apache2/other_vhosts_access.log"
                    sh "sudo grep -E ' (4|5)[0-9]{2} ' ${logFile} || echo 'No errors found yet'"
                }
            }
        }
    }
    
    post {
        always {
            echo 'Pipeline finished.'
        }
    }
}
