pipeline {
    agent any
    
    stages {
        stage('Checkout') {
            steps {
                // Haal de code op vanuit Git zonder specifieke credentials
                git branch: 'main', url: 'https://github.com/Wepsel/html3.git'
            }
        }
        
        stage('Deploy to Test Server') {
            when {
                // Voer dit stadium alleen uit voor bepaalde branches (bijv. develop)
                expression { currentBuild.rawBuild.getEnvironment(listener).get('BRANCH_NAME') == 'main' }
            }
            steps {
                // Kopieer HTML-bestanden naar de testserver via SSH
                bat 'echo Copying HTML files to test server'
                publishOverSSH(configName: 'test', transfers: [transfer(sourceFiles: '**/**', remoteDirectory: '/var/www/html')])
            }
        }
        
        stage('Deploy to Production Server') {
            when {
                // Voer dit stadium alleen uit voor bepaalde branches (bijv. master)
                expression { currentBuild.rawBuild.getEnvironment(listener).get('BRANCH_NAME') == 'main' }
            }
            steps {
                // Kopieer HTML-bestanden naar de productieserver via SSH
                bat 'echo Copying HTML files to production server'
                publishOverSSH(configName: 'prod-server-ssh-config', transfers: [transfer(sourceFiles: '*.html', remoteDirectory: '/path/on/prod/server')])
            }
        }
    }
}
