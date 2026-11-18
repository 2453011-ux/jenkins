
pipeline {
    agent any

    stages {

        stage('Checkout') {
            steps {
                echo 'Downloading code from GitHub'

                git branch: 'main',
                    url: 'https://github.com/2453011-ux/jenkins.git'
            }
        }

        stage('Validate') {
            steps {
                echo 'Validating HTML and CSS files'

                bat '''
                    if not exist index.html exit /b 1
                    if not exist style.css exit /b 1

                    echo HTML and CSS files found!
                '''
            }
        }

        stage('Build') {
            steps {
                echo 'Building Portfolio Website'

                bat '''
                    if not exist build mkdir build

                    copy /Y index.html build\\index.html
                    copy /Y style.css build\\style.css

                    echo Build completed successfully!
                '''
            }
        }

        stage('Deploy') {
            steps {
                echo 'Deploying Website'

                bat '''
                    if not exist C:\\JenkinsDeploy mkdir C:\\JenkinsDeploy

                    xcopy build\\* C:\\JenkinsDeploy\\ /E /I /Y

                    echo Deployment completed!
                '''
            }
        }
    }

    post {
        success {
            echo 'Pipeline executed successfully!'
        }

        failure {
            echo 'Pipeline failed!'
        }
    }
}
