pipeline {
agent any

stages {
stage('Compile') {
steps {
script {
bat "./mvnw.cmd clean compile -e"
}
}
}
stage('Test') {
steps {
script {
bat "./mvnw.cmd clean test -e"
}
}
}
stage('Jar') {
steps {
script {
sh "./mvnw clean package -e"
}
}
}

stage('Run') {
steps {
script {
bat "start /min mvnw.cmd spring-boot:run &&"
sleep 20
}
}
}
stage('TestApp') {
steps {
script {
bat "start chrome http://localhost:8081/rest/mscovid/test?msg=testing"
}
}
}
}
}
