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
