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
	stage('Push to DockerHub') {
	    steps {
		withCredentials([usernamePassword(credentialsId: 'dockerhub-creds', usernameVariable: 'USER', passwordVariable: 'PASS')]) {
			sh 'echo $USER'
		    sh 'echo $PASS | docker login -u $USER --password-stdin'
		    sh 'docker tag $IMAGE_NAME $USER/$IMAGE_NAME:latest'
		    sh 'docker push $USER/$IMAGE_NAME:latest'
		}
	    }
	}
  }
  environment {
    IMAGE_NAME = 'flask-api'
    CONTAINER_NAME = 'flask-api'
  }
}
