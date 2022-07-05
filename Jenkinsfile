node('test') {
  stages {
    stage('checkout') {
      steps {
        git 'https://github.com/vkarkad/website'
        sh "pwd && ls -la"
      }
    }
    stage('build') {
       echo "WORKSPACE: ${WORKSPACE}"
       echo "BUILD_NUMBER: ${BUILD_NUMBER}"
       echo "JOB_BASE_NAME: ${JOB_BASE_NAME}"
    }
  }
}
