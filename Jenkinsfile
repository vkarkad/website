job = env.JOB_BASE_NAME
num = env.BUILD_NUMBER
dir = '/opt/jenkins/workspace'

node('test') {
  stage('checkout') {
      git 'https://github.com/vkarkad/website'
      sh "pwd && ls -la"
  }
  stage('pre-build') {
      echo "WORKSPACE: ${dir}"
      echo "BUILD_NUMBER: ${num}"
      echo "JOB_BASE_NAME: ${job}"
  }
  stage('build') {
    sh "cd ${dir}/${job}"
    sh "sudo docker build . -t ${job}"
    sh "sudo docker run -dit --name web${num} -p 81:80 ${job}"
  }
}
