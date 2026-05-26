pipeline {
  agent any

  options {
    timestamps()
  }

environment {
    // Local image names (later we will change to ECR/DockerHub)
    BACKEND_IMAGE  = "ecommerce-backend"
    FRONTEND_IMAGE = "ecommerce-frontend"
  }

  stages {
    stage('Checkout') {
      steps {
        checkout scm
        sh 'echo "✅ Code checked out successfully"'
      }
    }

    stage('Info') {
      steps {
        sh '''
          echo "✅ Jenkins is executing pipeline"
          echo "Branch: ${BRANCH_NAME}"
          echo "Build Number: ${BUILD_NUMBER}"
          echo "Workspace: ${WORKSPACE}"
          ls -la
        '''
      }
    }
  //  stage('Set Version Tag') {
      //   steps {
        //    script {
      // Short Git commit id
                  // def commit = sh(script: "git rev-parse --short HEAD", returnStdout: true).trim()

      // Version format (MNC style): buildNumber-commit
     // env.IMAGE_TAG = "${BUILD_NUMBER}-${commit}"

      //echo "✅ Version Tag Generated: ${env.IMAGE_TAG}"
    //}
    stage('Set Version Tag') {
  steps {
    script {
      env.IMAGE_TAG = "${BUILD_NUMBER}"
      echo "✅ Version Tag: ${env.IMAGE_TAG}"
            }
         }
        }
       
  stage('Build Backend Docker Image') {
      steps {
        dir('backend') {
          sh """
            echo "Building backend image..."
            docker build -t ${BACKEND_IMAGE}:${IMAGE_TAG} -t ${BACKEND_IMAGE}:latest .
          """
        }
      }
    }

stage('Build Frontend Docker Image') {
      steps {
        dir('frontend') {
          sh """
            echo "Building frontend image..."
            docker build -t ${FRONTEND_IMAGE}:${IMAGE_TAG} -t ${FRONTEND_IMAGE}:latest .
          """
        }
      }
    }

  
}

  

  post {
    success {
      echo "✅ Pipeline basic test SUCCESS"
    }
    failure {
      echo "❌ Pipeline basic test FAILED"
    }
  }
}
