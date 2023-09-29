pipeline {
    agent any
    
    stages {
        stage('Checkout') {
            steps {
                // Haal de broncode op van GitHub
                bat 'git clone https://github.com/Wepsel/html3.git'
            }
        }
        
        stage('Deploy to Test Server') {
            steps {
                // Kopieer de HTML-bestanden naar de testserver
                bat 'xcopy /E /I html\\* student@10.0.0.26:\\var\\www\\html\\'
            }
        }
        
        stage('Deploy to Production Server') {
            steps {
                // Kopieer de HTML-bestanden naar de productieserver
                bat 'xcopy /E /I html\\* user@productionserver:\\path\\to\\deploy\\'
            }
        }
    }
}
