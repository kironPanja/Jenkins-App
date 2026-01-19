pipeline {
    agent any

    stages {
        stage('Pull from GitHub') {
            steps {
                git branch: 'main',
                    url: 'https://github.com/kironPanja/Jenkins-App.git',
                    credentialsId: 'github-creds'
            }
        }

        stage('Copy to Nginx HTML Folder') {
            steps {
                bat '''
                REM Copy files from Jenkins workspace to Nginx HTML folder
                xcopy "%WORKSPACE%\\*" "C:\\ProgramData\\nginx\\html\\" /E /I /Y

                REM Start Nginx manually (if not running as a service)
                cd C:\\ProgramData\\nginx
                start nginx
                '''
            }
        }
    }

    post {
        success {
            echo '✅ Files successfully deployed to Nginx!'
        }
        failure {
            echo '❌ Pipeline failed. Check logs for details.'
        }
    }
}
