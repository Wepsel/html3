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
                expression { currentBuild.rawBuild.getEnvironment().get('BRANCH_NAME') == 'main' }
            }
            steps {
                echo 'Copying HTML files to the test server'
                bat 'echo y | pscp -pw student C:\\ProgramData\\Jenkins\\.jenkins\\workspace\\Multibranch_main\\*.html student@10.0.0.26:/var/www/html/'
            }
        }

        stage('Deploy to Production Server') {
            when {
                expression { currentBuild.rawBuild.getEnvironment().get('BRANCH_NAME') == 'master' }
            }
            steps {
                echo 'Copying HTML files to the production server'
                bat 'echo y | pscp -pw student C:\\ProgramData\\Jenkins\\.jenkins\\workspace\\Multibranch_main\\*.html student@10.0.0.27:/var/www/html/'
            }
        }
    }
}
