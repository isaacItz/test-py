pipeline {
    agent any

    environment {
        IMAGE_NAME = "flask-api"
        CONTAINER_NAME = "flask-api"
    }

    stages {
        stage('Checkout') {
            steps {
                echo 'Clonando repositorio...'
                checkout scm
            }
        }
        stage('Build Docker image') {
            steps {
                echo 'Construyendo imagen Docker...'
                sh 'docker build -t $IMAGE_NAME .'
            }
        }
        stage('Run Container') {
            steps {
                echo 'Iniciando contenedor...'
                // Detiene contenedor anterior si existe
                sh 'docker stop $CONTAINER_NAME || true && docker rm $CONTAINER_NAME || true'
                // Inicia nuevo contenedor
                sh 'docker run -d --name $CONTAINER_NAME -p 5000:5000 $IMAGE_NAME'
            }
        }
    }
}
