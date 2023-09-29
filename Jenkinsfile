pipeline {
    agent any
    
    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/Wepsel/html3.git'
            }
        }
        
        stage('Deploy to Test Server') {
            when {
                expression { currentBuild.rawBuild.getEnvironment(listener).get('BRANCH_NAME') == 'main' }
            }
            steps {
                echo 'Copying HTML files to the test server'
                // SSH-copy HTML-bestanden naar de testserver met wachtwoord
                bat 'echo y | plink -pw student student@10.0.0.26 "cd /var/www/html && put *.html"'
            }
        }
        
        stage('Deploy to Production Server') {
            when {
                expression { currentBuild.rawBuild.getEnvironment(listener).get('BRANCH_NAME') == 'main' }
            }
            steps {
                echo 'Copying HTML files to the production server'
                // SSH-copy HTML-bestanden naar de productieserver met wachtwoord
                bat 'echo y | plink -pw your_ssh_password user@prod_server_ip "cd /path/on/prod/server && put *.html"'
            }
        }
    }
}
