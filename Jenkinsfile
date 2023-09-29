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
                bat 'sshpass -p "student" scp -r *.html student@10.0.0.26:/var/www/html/'
            }
        }
        
        stage('Deploy to Production Server') {
            when {
                expression { currentBuild.rawBuild.getEnvironment(listener).get('BRANCH_NAME') == 'main' }
            }
            steps {
                echo 'Copying HTML files to the production server'
                // SSH-copy HTML-bestanden naar de productieserver met wachtwoord
                bat 'sshpass -p "your_ssh_password" scp -r *.html user@prod_server_ip:/path/on/prod/server/'
            }
        }
    }
}
