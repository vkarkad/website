BUILD_JOB = env.JOB_BASE_NAME
BUILD_NUM = env.BUILD_NUMBER
BUILD_DIR = '/opt/jenkins/workspace'
PUBLIC_IP = ''
CNTR_PORT = 80
HOST_PORT = CNTR_PORT + env.BUILD_NUMBER.toInteger()
IMAGE_NAME = 'web'
MAJOR_VER = '1'
IMAGE_VER = MAJOR_VER + '.' + env.BUILD_NUMBER

node('test') {
  stage('checkout') {
    git branch: 'test', url: 'https://github.com/vkarkad/website.git'
    sh "pwd && ls -la"
  }
  stage('pre-build') {
    ip_cmd = "curl ifconfig.co | tail -1"
    PUBLIC_IP = sh (script: ip_cmd, returnStdout: true).trim()
    echo "PUBLIC_IP: <<${PUBLIC_IP}>>"
    echo "HOST_PORT: <<${HOST_PORT}>>"
    echo "CNTR_PORT: <<${CNTR_PORT}>>"
    echo "IMAGE_VER: <<${IMAGE_VER}>>"
    echo "WORKSPACE: <<${BUILD_DIR}>>"
    echo "BUILD_NUMBER: <<${BUILD_NUM}>>"
    echo "JOB_BASE_NAME: <<${BUILD_JOB}>>"
  }
  stage('build') {
    sh "cd ${BUILD_DIR}/${BUILD_JOB};pwd;ls -l;cat -n Dockerfile"
    IMAGE_TAG = "${BUILD_JOB}:${IMAGE_VER}"
    sh "sudo docker build --tag ${IMAGE_TAG} ."
    sh "sudo docker run -dit --name ${BUILD_JOB}${BUILD_NUMBER} -p ${HOST_PORT}:${CNTR_PORT} ${IMAGE_TAG}"
  }
  stage('publish') {
    echo "Website URL: http://${PUBLIC_IP}:${HOST_PORT}"
  }
}
