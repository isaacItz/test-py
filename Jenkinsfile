pipeline {
  agent any
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
	sh  'ls'
        sh 'docker build -t $IMAGE_NAME .'
      }
    }

    stage('Run Container') {
      steps {
        echo 'Iniciando contenedor...'
        sh 'docker stop $CONTAINER_NAME || true && docker rm $CONTAINER_NAME || true'
        sh 'docker run -d --name $CONTAINER_NAME -p 5000:5000 $IMAGE_NAME'
      }
    }

  }
  environment {
    IMAGE_NAME = 'flask-api'
    CONTAINER_NAME = 'flask-api'
  }
}
