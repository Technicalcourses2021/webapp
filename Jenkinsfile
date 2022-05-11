pipeline {
    agent any

    stages {
        stage('Git Checkout') {
            steps {
                git credentialsId: 'jenkinsGitHub', url: 'https://github.com/Technicalcourses2021/webapp.git'
            }
        }
        stage('mvn configuration') {
            steps {
                withMaven(maven: 'M2_HOME') {
                    sh 'mvn clean install'
                    }
            }
        }
        stage('docker image build') {
            steps {
                sh 'docker build -t sudheer10thota/webapp:1.0.0 .'
            }
        }
        /*stage('Push Docker Image') {
            steps {
                withCredentials([string(credentialsId: 'jenkinsdocker-hub-pwd', variable: 'dockerhubpwd')]) {
             sh "docker login -u sudheer10thota -p ${dockerhubpwd}"
            }
            sh 'docker push sudheer10thota/webapp:1.0.0'
            }
        } */
        /*stage('Run your image'){
            steps {
                sh 'docker run -dit -p 8003:8080 sudheer10thota/webapp:1.0.0'
            }
        }*/
    }
}
