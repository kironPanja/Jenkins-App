
pipeline {
    agent any

    stages {
        stage('Pull from GitHub') {
            steps {
                git branch: 'main',
                    url: 'https://github.com/kironPanja/wipro-devops-repo.git',
                    credentialsId: 'github-creds'
            }
        }

        stage('Copy to Nginx HTML Folder') {
            steps {
                bat '''
                xcopy "%WORKSPACE%\\*" "C:\\nginx\\html\\" /E /I /Y
                net stop nginx
                net start nginx
                '''
            }
        }
    }

    post {
        success {
            echo '✅ Files copied to Nginx successfully!'
        }
        failure {
            echo '❌ Pipeline failed. Please check logs for errors.'
        }
    }
}
