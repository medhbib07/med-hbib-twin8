pipeline {
    agent any

    tools {
        jdk 'JAVA_HOME'
        maven 'M2_HOME'
    }

    stages {
        stage('GIT') {
            steps {
                git branch: 'master', url: 'https://github.com/medhbib07/med-hbib-twin8.git'
            }
        }

        stage('Compile Stage') {
            steps {
                sh 'mvn clean package'
            }
        }
        stage('Build image') {
            steps {
                sh 'docker build -t medhbib07/med-hbib-twin8:latest .'
            }
        }
        stage('Login to DockerHub') {
            steps {
                withCredentials([usernamePassword(credentialsId: 'dockerhub-medhbib07', passwordVariable: 'dckr_pat_odpynls-t1ZlEoGLXtqH2JKL0pY', usernameVariable: 'hbibworld')]) {
                    sh 'echo $dckr_pat_odpynls-t1ZlEoGLXtqH2JKL0pY | docker login -u $hbibworld --password-stdin'
                }
            }
        }
        stage('Push image') {
            steps {
                 sh 'docker push medhbib07/med-hbib-twin8:latest'
            }
        }
    }
}
