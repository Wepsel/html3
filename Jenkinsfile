pipeline {
    agent any
    
    options {
        skipDefaultCheckout(true)  // Sla de standaard checkout over
    }
    
    stages {
        stage('Set Workspace Path') {
            steps {
                // Handmatig het pad naar de workspace instellen
                dir("C:\\ProgramData\\Jenkins\\.jenkins\\workspace\\Multibranch_main") {
                    // Haal de broncode op van GitHub
                    git url: 'https://github.com/Wepsel/html3.git'
                }
            }
        }
        
        stage('Deploy to Test Server') {
            steps {
                // Geef het absolute pad naar de HTML-bestanden op
                def sourceDir = bat(script: 'echo %WORKSPACE%\\html', returnStdout: true).trim()
                def targetDir = 'student@10.0.0.26:\\var\\www\\html\\'
                
                // Kopieer de HTML-bestanden naar de testserver
                bat "xcopy /E /I ${sourceDir}\\* ${targetDir}"
            }
        }
        
        stage('Deploy to Production Server') {
            steps {
                // Geef het absolute pad naar de HTML-bestanden op
                def sourceDir = bat(script: 'echo %WORKSPACE%\\html', returnStdout: true).trim()
                def targetDir = 'user@productionserver:\\path\\to\\deploy\\'
                
                // Kopieer de HTML-bestanden naar de productieserver
                bat "xcopy /E /I ${sourceDir}\\* ${targetDir}"
            }
        }
    }
}
