pipeline {
    agent any
    
    stages {
        stage('Checkout') {
            steps {
                git branch: 'test', url: 'https://github.com/Wepsel/html3.git'
            }
        }
        
        stage('Deploy to Test Server') {
            when {
                expression { currentBuild.rawBuild.getEnvironment().get('BRANCH_NAME') == 'test' }
            }
            steps {
                echo 'Copying HTML files to the test server'
                bat 'echo y | pscp -pw student C:\\ProgramData\\Jenkins\\.jenkins\\workspace\\Multibranch_test\\*.html student@10.0.0.26:/var/www/html/'
            }
        }
    }
}
