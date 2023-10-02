pipeline {
    agent any
    
    stages {
        stage('Checkout') {
            steps {
                git branch: 'master', url: 'https://github.com/Wepsel/html3.git'
            }
        }

        stage('Deploy to Production Server') {
            when {
                expression { currentBuild.rawBuild.getEnvironment().get('BRANCH_NAME') == 'master' }
            }
            steps {
                echo 'Copying HTML files to the production server'
                bat 'echo y | pscp -pw student C:\\ProgramData\\Jenkins\\.jenkins\\workspace\\Multibranch_master\\*.html student@10.0.0.27:/var/www/html/'
            }
            post {
                always {
                    input "Do you want to proceed with the deployment to the production server?"
                }
            }
        }
    }
}
