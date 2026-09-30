pipeline {
 environment {
 imagename = "prajuldocker/mask-web1" // change the docker and image name
 image_tag    = "${BUILD_NUMBER}" // Sets version to current Jenkins build number
 registryCredential = 'praju.keeriyat@gmail.com' // docker credentails
 dockerImage = ''
 }
 agent any
 stages {
 stage('Cloning Git') {
 steps {
 git([url: 'git@github.com:prajulkeeriyat/jenkins-repo-prajul-latest.git', branch: 'main']) // change the git url
 }
 }
 stage('Building image') {
 steps{
 script {
 dockerImage = docker.build imagename
 }
 }
 }
 stage('Running image') {
 steps{
 script {
 sh "docker run -itd -P ${imagename}:latest"
 }
 }
 }
 stage('Deploy Image') {
 steps{
 script {
 docker.withRegistry( '', registryCredential ) {
 dockerImage.push("$BUILD_NUMBER")
 dockerImage.push('latest')
 }
 }
 }
 }
 }
}
