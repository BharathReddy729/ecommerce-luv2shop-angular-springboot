pipeline {
  agent any

  options {
    timestamps()
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
