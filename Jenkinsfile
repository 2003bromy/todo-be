pipeline {
    agent any
    stages {
        stage('Build stage') {
            steps {
              echo "Build Stage is running for be"
              sh 'DOCKER_BUILDKIT=1 docker build -f Dockerfile-pipelines -t romy2003-builder-be --target builder .'
            }
        }
        stage('Delivery stage') {
            steps {
                echo "Delivery Stage is running for be" 
                sh 'DOCKER_BUILDKIT=1 docker build -f Dockerfile-pipelines -t romy2003/todo-be:jenkins-$BUILD_NUMBER --target delivery .'
            }
        }
        stage('Cleanup') {
            steps {
                echo "Cleanup-stage is running for be"
                sh 'docker system prune -f'
            }
        }
        stage('Push to Docker') {
            environment {
                dockerpwd = credentials('AlexDoc')
            }
            steps {
                echo "Push to Docker"
                sh 'docker login -u romy2003 -p ${dockerpwd}'
                sh "docker push romy2003/todo-be:jenkins-$BUILD_NUMBER"
            }
        }
    }
}
