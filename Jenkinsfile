pipeline {
    agent any
    stages {
        stage('Build') {
            steps {
                echo 'Building the master branch...'
            }
        }
        stage('Test') {
            steps {
                echo 'Testing the master branch...'
            }
        }
        stage('Deploy') {
            steps {
                echo 'Deploying the master branch...'
                sh '''
                # Create the deployment directory
                mkdir -p /tmp/deployment_directory_master

                # Copy the index.html file from the Jenkins workspace
                cp $WORKSPACE/intedx.html /tmp/deployment_directory_master/

                # Start the Python HTTP server on port 9090
                nohup python3 -m http.server 9090 --directory /tmp/deployment_directory_master > /tmp/server_master.log 2>&1 &
                '''
                echo "Master branch page is being served on http://localhost:9090"
            }
        }
        stage('Archive HTML') {
            steps {
                archiveArtifacts artifacts: '*.html', fingerprint: true
            }
        }
    }
}

