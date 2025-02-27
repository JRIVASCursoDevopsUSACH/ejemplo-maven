pipeline {
agent any
environment {
        SONAR_TOKEN = credentials('sonar-key')}

stages {
stage('Compile') {
steps {
script {
bat "./mvnw.cmd clean compile -e"
}
}
}
stage('SonarQube Analysis') {
            steps {
                script {
                    def scannerHome = tool 'Sonar-scanner'
                    bat "${scannerHome}/bin/sonar-scanner -Dsonar.projectKey=ejemplo-maven -Dsonar.java.binaries=build -Dsonar.sources=. -Dsonar.host.url=http://localhost:9000 -Dsonar.login=${env.SONAR_TOKEN}"
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
bat "./mvnw clean package -e"
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
