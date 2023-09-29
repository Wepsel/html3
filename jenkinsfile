pipeline {
    agent any
    
    stages {
        stage('Checkout') {
            steps {
                // Haal de broncode op van GitHub
                git url: 'https://github.com/Wepsel/html.git'
            }
        }
        
        stage('Deploy to Test Server') {
            steps {
                // Kopieer de HTML-bestanden naar de testserver
                sh 'rsync -avz ./html/* student@10.0.0.26:/pvar/www/html/'
            }
        }
        
        stage('Deploy to Production Server') {
            steps {
                // Kopieer de HTML-bestanden naar de productieserver
                sh 'rsync -avz ./html/* user@productionserver:/path/to/deploy/'
            }
        }
    }
}
