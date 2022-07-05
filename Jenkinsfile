job = env.JOB_BASE_NAME
num = env.BUILD_NUMBER
dir = '/opt/jenkins/workspace'
PUBLIC_IP = ''
HOST_PORT = 80 + env.BUILD_NUMBER

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
      echo "WORKSPACE: <<${dir}>>"
      echo "BUILD_NUMBER: <<${num}>>"
      echo "JOB_BASE_NAME: <<${job}>>"
  }
  stage('build') {
    sh "cd ${dir}/${job};pwd;ls -l;cat -n Dockerfile"
    sh "sudo docker build -t ${job} ."
    sh "sudo docker run -dit --name web${num} -p 81:80 ${job}"
  }
}
