pipeline {
    agent any
    stages {
        stage('Build') {
            steps {
                echo 'Building the login page branch...'
            }
        }
        stage('Test') {
            steps {
                echo 'Testing the login page branch...'
            }
        }
        stage('Deploy') {
            steps {
                echo 'Deploying the login page...'
                sh '''
                # Create the deployment directory
                mkdir -p /tmp/deployment_directory_login

                # Check if login.html exists
                if [ ! -f ${WORKSPACE}/login.html ]; then
                    echo "Error: login.html not found in workspace."
                    exit 1
                fi

                # Copy the login.html file from the Jenkins workspace
                cp ${WORKSPACE}/login.html /tmp/deployment_directory_login/

                # Start the Python HTTP server on port 9191
                nohup python3 -m http.server 9191 --directory /tmp/deployment_directory_login > /tmp/server_login.log 2>&1 &
                '''
                echo "Login page is being served on http://localhost:9191"
            }
        }
        stage('Archive HTML') {
            steps {
                archiveArtifacts artifacts: '*.html', fingerprint: true
            }
        }
    }
}

