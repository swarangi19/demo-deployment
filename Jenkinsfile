pipeline {
    agent any
    stages {
        stage('Build') {
            steps {
                git branch: 'main', url: 'https://github.com/swarangi19/demo-deployment.git'
                sh 'docker build -t newimg .'
            }
            post {
                success {
                    echo "Build Successful"
                }
            }
        }
        stage('Run') {
            steps {
                sh '''
                CONTAINER_NAME="my-app-container"
                IMAGE_NAME="newimg"

                # Check if the container exists
                if [ "$(docker ps -aq -f name=^/${CONTAINER_NAME}$)" ]; then
                    echo "Container '${CONTAINER_NAME}' already exists. Skipping run."
                    docker rm -f ${CONTAINER_NAME}
                fi
                    echo "Container '${CONTAINER_NAME}' not found. Starting it now..."
                    docker run -d --name "${CONTAINER_NAME}" "${IMAGE_NAME}"
                    echo "Container started successfully."
                
                '''
            }
            post {
                success {
                    echo "Run successful"
                }
            }
        }
    }
}
